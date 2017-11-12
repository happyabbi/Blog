title: C# - Note
categories:
- C#
tags:
- C#
---

## ctor 
快速建立Class的Constructor

##cw
快速建立Console.WriteLine();

## modifer 

public -> EveryWhere
private -> only in the same class
internal -> only in the same assembly

## Delegate

``` C#
public delegate void NameChangedDelegate(string existingName, string newName);  
```

``` C#
public class GradeBook
{
    public static float MinimumGrade = 0;
    public static float MaximumGrade = 100;

    public GradeStatistics ComputeStatistics()
    {
        GradeStatistics stats =  new GradeStatistics();

        float sum = 0;
        foreach (var grade in grades)
        {
            stats.HighestGrade = Math.Max(grade, stats.HighestGrade);
            stats.LowestGrade = Math.Min(grade, stats.LowestGrade);
            sum += grade;
        }

        stats.AverageGrade = sum / grades.Count;


        return stats;
    }

    List<float> grades;

    public void AddGrade(float grade){
        grades.Add(grade);
    }

    public GradeBook()
    {
        _name = "Empty";
        grades = new List<float>();
    }

    public NameChangedDelegate NameChanged;
    private string _name;
    public string Name
    {
        get
        {
            return _name;
        }
        set{
            if(!string.IsNullOrEmpty(value))
            {
                if(_name != value)
                {
                    NameChanged(_name, value);
                }
                _name = value;                   
            }
            }
    }
} 
```


``` C#
class MainClass
{
    public static void Main(string[] args)
    {
        GradeBook book = new GradeBook
        {
            NameChanged = new NameChangedDelegate(OnNameChanged),
            Name = "Scott's Grade Book"
        };
        book.Name = "Grade Book";

        book.Name = null;
        book.AddGrade(91);
        book.AddGrade(89.5f);
        book.AddGrade(75);
        GradeStatistics stats = book.ComputeStatistics();

        Console.WriteLine(book.Name);
        WriteResult("Average" , stats.AverageGrade);
        WriteResult("Highest" , (int)stats.HighestGrade);
        WriteResult("Lowest" , stats.LowestGrade);
    }

    static void OnNameChanged(string existingName,string newName){
        Console.WriteLine($"Grade book changing name from {existingName} to {newName}");
    }

    static void WriteResult(string description, int result)
    {
        Console.WriteLine(description + ": " + result);
    }

    static void WriteResult(string description,  float result){
        Console.WriteLine($"{description}: {result:F2}");
    }
}
```


## Event Revisited

``` C#
  public class GradeStatistics
	{
		public float AverageGrade;
		public float HighestGrade;
		public float LowestGrade;


		public GradeStatistics()
        {
            HighestGrade = 0;
            LowestGrade = float.MaxValue;
        }
    }
```

``` C#
 public delegate void NameChangedDelegate(object sendor, NameChangedEventArgs args);
```

``` C#
  public class NameChangedEventArgs :EventArgs
    {
        public string ExistingName
        {
            get;
            set;
        }

        public string NewName
        {
            get;
            set;
        }
    }
```

``` C#
 public class GradeBook
    {
        public static float MinimumGrade = 0;
        public static float MaximumGrade = 100;

        public GradeStatistics ComputeStatistics()
        {
            GradeStatistics stats =  new GradeStatistics();

            float sum = 0;
            foreach (var grade in grades)
            {
                stats.HighestGrade = Math.Max(grade, stats.HighestGrade);
                stats.LowestGrade = Math.Min(grade, stats.LowestGrade);
                sum += grade;
            }

            stats.AverageGrade = sum / grades.Count;


            return stats;
        }

        List<float> grades;

        public void AddGrade(float grade){
            grades.Add(grade);
        }

        public GradeBook()
        {
            _name = "Empty";
            grades = new List<float>();
        }

        public event NameChangedDelegate NameChanged;

        private string _name;
        public string Name
        {
            get
            {
                return _name;
            }
            set{
                if(!string.IsNullOrEmpty(value))
                {
                    if(_name != value)
                    {
                        NameChangedEventArgs args = new NameChangedEventArgs();
                        args.ExistingName = _name;
                        args.NewName = value;
                        
                        NameChanged(this, args);
                    }
                    _name = value;                   
                }
             }
        }
    }
```

``` C#
 class MainClass
    {
        public static void Main(string[] args)
        {
            GradeBook book = new GradeBook();
            book.NameChanged += OnNameChanged;

            book.Name = "Scott's Grade Book";
            book.Name = "Grade Book";

            book.Name = null;
            book.AddGrade(91);
            book.AddGrade(89.5f);
            book.AddGrade(75);
            GradeStatistics stats = book.ComputeStatistics();

            Console.WriteLine(book.Name);
            WriteResult("Average" , stats.AverageGrade);
            WriteResult("Highest" , (int)stats.HighestGrade);
            WriteResult("Lowest" , stats.LowestGrade);
        }

        static void OnNameChanged(object sender, NameChangedEventArgs args){
            Console.WriteLine($"Grade book changing name from {args.ExistingName} to {args.NewName}");
        }

        

        static void WriteResult(string description, int result)
        {
            Console.WriteLine(description + ": " + result);
        }

        static void WriteResult(string description,  float result){
            Console.WriteLine($"{description}: {result:F2}");
        }
    }
```