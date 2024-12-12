see: [[Custom Model Binder]] for explanation
```c#
public class OrderModelBinder : IModelBinder
{
	public Task BindModelAsync(ModelBindingContext bindingContext)
	{
		var orderNo = bindingContext.ValueProvider.GetValue("OrderNo");
		var orderDate = bindingContext.ValueProvider.GetValue("OrderDate");
	
		//bind both values into order model
		var order = new Order
		{
			OrderNo = Convert.ToInt32(orderNo.FirstValue),
			OrderDate = Convert.ToDateTime(orderDate.FirstValue)
		};
		
		if (orderNo == ValueProviderResult.None)
		{
			order.OrderNo = Guid.NewGuid().GetHashCode();
			bindingContext.Result = ModelBindingResult.Success(order);
			return Task.CompletedTask;
		}
	
		bindingContext.Result = ModelBindingResult.Success(order);
		return Task.CompletedTask;
	}  
}
```
In the sample above we binded both `OrderNo` and `OrderDate` but only modify the `OrderNo`. If we don't bind `OrderDate` it will not be read by the controller