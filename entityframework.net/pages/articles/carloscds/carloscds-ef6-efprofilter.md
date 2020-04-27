---
Permalink: articles/carloscds-ef6-efprofilter
name: EF6 - EFProfiler
tags: carloscds article profiler
OriginalLink: http://carloscds.net/2010/08/efprofiler-entity-framework-profiler/
CreatedDate: 2010-08-20
CreatedUserName: Carlos dos Santos
CreatedUserLink: http://carloscds.net/
---

# EFProfiler - Entity Framework Profiler

If you are working with EF4, you have probably wondered if the generated SQL commands are really optimized, or maybe when you have a performance problem. To answer that, several analysis tools or profilers exist, and one of these is the `EFProfiler`.

The tool is quite simple. You download an executable from the website [EF Profiler](https://hibernatingrhinos.com/products/EFProf) and follow the instructions contained in the file "How to use.txt".

For the profiler to work, you need to add a Profiler DLL reference to your project:

<img src="http://carloscds.net/wp-content/uploads/2010/08/image_thumb2.png" width="339" height="206">

Then, in the main project file, you run the profiler initializer:

```csharp
static void Main(string[] args)
{
    // Profiler
    HibernatingRhinos.Profiler.Appender.EntityFramework.EntityFrameworkProfiler.Initialize();

    TesteEntities dc = new TesteEntities();

    var datas = from c in dc.Client
                select c;
                
    foreach (var data in datas)
    {
        Console.WriteLine(data.Name);
    }
}
```

In the example above, we have a simple query to the database.

Now open the profiler and run your application, the results will appear on the screen:

<img src="http://carloscds.net/wp-content/uploads/2010/08/image_thumb4.png" width="883" height="469">

That's it folks, a good profiler for you!