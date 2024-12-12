Most common way to create Web API Request Methods  and some guidelines:
#### GET
Get is straightforward, either they return [[NotFound()]] or they return the found object:
```c#
//get a list of cities
[HttpGet]
public async Task<IActionResult> GetCities() 
{
	if (_context.Cities == null)
	{
		return NotFound();
	}
	
	var cities = await _context.Cities.OrderBy(temp => temp.CityName).ToListAsync(); 
	return Ok(cities); 
}

//get one city only
[HttpGet("{cityID}")]
public async Task<IActionResult> GetCity(Guid cityID)
{
	var city = await _context.Cities.FirstOrDefaultAsync(temp => temp.CityID == cityID);
	
	if (city == null)
	{
		return NotFound();
	}
	
	return Ok(city);
}
```
>[!warning]
>These are just samples that directly access the DB context, in real world, you might access a service or a repository instead.
#### PUT
>[!warning] Important
>Use [[Bind and BindNever]] in order to secure against attackers overposting on POST and PUT methods.
```c#
[HttpPut("{cityID}")]
public async Task<IActionResult> PutCity(Guid cityID, [Bind(nameof(City.CityID), nameof(City.CityName))] City city)
	//if the Bind confused you, see Bind and BindNever note.
{
	if (cityID != city.CityID) 
	{
		var problemDetails = new ProblemDetails
        {
            Title = "Invalid request",
            Status = 400, //400 bad request
            Detail = "City data is missing or invalid.",
            Instance = HttpContext.Request.Path
        };
		
		return Problem(problemDetails); 
			//see Problem() note for more details.
	}
	
	var existingCity = await _context.Cities.FindAsync(cityID);
		//if it exist, get it
		
	if (existingCity == null)
	{
		//If it does not, then 404 not found
		return NotFound(); //HTTP 404
	}
	
	existingCity.CityName = city.CityName;
	//If its found then update it and catch some errors while youre at it
	//DISCLAIMER: This is just a sample, usually this is done in the repository
	try
	{
		await _context.SaveChangesAsync();
	}
	catch (DbUpdateConcurrencyException)
	{
		if (!CityExists(cityID))
		{
			return NotFound();
		}
		else
		{
			throw;
		}
	}
	
	return NoContent();
		//returns NoContent since PUT is just a process, and no content is needed to return, only success.
		//see NoContent() note for more details.
}
```
#### POST
```c#
[HttpPost]
public async Task<IActionResult> PostCity([Bind(nameof(City.CityID), nameof(City.CityName))] City city)
{
    if (_context.Cities == null)
    {
        var problemDetails = new ProblemDetails
        {
            Title = "not found",
            Status = 404, // Not found
            Detail = "Entity set 'ApplicationDbContext.Cities' is null",
            Instance = HttpContext.Request.Path
        };
        
        return Problem(problemDetails);
	        // See Problem() note.
    }
    
    _context.Cities.Add(city);
    await _context.SaveChangesAsync();
    
    return CreatedAtAction("GetCity", new { cityID = city.CityID }, city);
	    // CreatedAtAction is the return used for API POST method, see CreatedAtAction() note for more details.
}
```
#### Delete
```c#
[HttpDelete("{id}")]
// DELETE: api/Cities/5
[HttpDelete("{id}")]
public async Task<IActionResult> DeleteCity(Guid id)
{
	var city = await _context.Cities.FindAsync(id); //get the city
	if (city == null)
	{
		return NotFound(); //if null then 404 not found
	}
	
	_context.Cities.Remove(city); //if found mark it for removal
	await _context.SaveChangesAsync(); //save changes
	
	return NoContent(); //HTTP 200
		//returns NoContent since DELETE is just a process, and no content is needed to return, only success.
		//see NoContent() note for more details.
}
```
>[!warning]
>Again these are just samples where DbContext is directly accessd, the processes here are usually done in a repository or service
# What next:
- [[Problem()]] - might need to know this for the errors.
- when returning errors, use already made methods, don't forget what those are, see: [[IActionResult]].