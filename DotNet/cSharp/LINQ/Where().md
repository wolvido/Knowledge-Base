#cSharp 
syntax:
```c#
public static IEnumerable<TSource> Where<TSource>(this IEnumerable<TSource> source, Func<TSource, bool> predicate)
        {
            if (source == null)
            {
                throw Error.ArgumentNull("source");
            }
 
            if (predicate == null)
            {
                throw Error.ArgumentNull("predicate");
            }
 
            if (source is Iterator<TSource>)
            {
                return ((Iterator<TSource>)source).Where(predicate);
            }
 
            if (source is TSource[])
            {
                return new WhereArrayIterator<TSource>((TSource[])source, predicate);
            }
 
            if (source is List<TSource>)
            {
                return new WhereListIterator<TSource>((List<TSource>)source, predicate);
            }
 
            return new WhereEnumerableIterator<TSource>(source, predicate);
        }
```
// Summary:
//     Filters a sequence of values based on a predicate. Each element's index is used
//     in the logic of the predicate function.
//
// Parameters:
//   source:
//     An System.Collections.Generic.IEnumerable`1 to filter.
//
//   predicate:
//     A function to test each source element for a condition; the second parameter
//     of the function represents the index of the source element.
//
// Type parameters:
//   TSource:
//     The type of the elements of source.
//
// Returns:
//     An System.Collections.Generic.IEnumerable`1 that contains elements from the input
//     sequence that satisfy the condition.
//
// Exceptions:
//   T:System.ArgumentNullException:
//     source or predicate is null.