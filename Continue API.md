# Paging

 #### info

 is a way to provide partial data from api when having big result to be delivered in this case it would be ineffective to send the date everytime such request comes.
 when using paging you can deliver a set amout of result (Pagesize) and provide a way to fetch more on request (nextPage)

 #### apply
 create a helper class to help with all the page data

 ```cs
 public class PageData 
 {
         public int CurrentPage { get; set; }     
         public int TotalPages { get; set; }     
         public int PageSize { get; set; }     
         public int TotalCount { get; set; }      
         public bool HasPrevious => CurrentPage > 1;     
         public bool HasNext => CurrentPage < TotalPages; 
} 
 ```


```cs
public class PagedList<T> : List<T> 
{     
    public PageData PageData { get; set; }      
    public PagedList(List<T> items, int count, int pageNumber, int pageSize)     
    {         
        PageData = new PageData         
        {             
            TotalCount = count,             
            PageSize = pageSize,             
            CurrentPage = pageNumber,             
            TotalPages = (int)Math.Ceiling(count / (double)pageSize)         
        };          
        AddRange(items);     
    }      
    public static PagedList<T> ToPagedList(IEnumerable<T> source, int pageNumber, int pageSize)     
    {         
        var count = source.Count();         
        var items = source             
                    .Skip((pageNumber - 1) * pageSize)             
                    .Take(pageSize).ToList(); 
        return new PagedList<T>(items, count, pageNumber, pageSize); 
    } 
}
```



# Filtering

# Searching

# Sorting 

# Data Shaping

# HATEOAS