# Matched and one not Condition

## Description

The `MatchedAndOneNotCondition` option lets you perform or skip the update action, depending on if at least one value for the source is different than the destination for properties specified.

### Example

```csharp
context.BulkMerge(customers, options => 
{
	// USE the code as the key expression
	options.ColumnPrimaryKeyExpression = x => x.Code;
	
	// ON UPDATE, modify customers only that has the same `IsLocked` value (always 0 on the source)
	options.MergeMatchedAndConditionExpression = x => new { x.IsLocked };
});
```

## Scenario

A company uses Entity Framework and needs to import customers with the `BulkMerge` method to insert new customers and update existing customers.

However, there is a particularity. The `Note` column is not really important and should not perform an update action if this is the only value that has been modified.

The update action should only be performed if another values such as the `Code` or `Name` has been modified.

In summary:

- If only the `Note` value is different, we don't want to update the customer.
- If any value specified in the `MatchedAndOneNotCondition` option is different, we want to update the customer

## Solution

The`MatchedAndOneNotCondition` option have 4 solutions to this problem:

- [[Action]MatchedAndOneNotConditionExpression](#actionmatchedandonenotconditionexpression)
- [[Action]MatchedAndOneNotConditionNames](#actionmatchedandonenotconditionnames)
- [IgnoreOn[Action]MatchedAndOneNotConditionExpression](#ignoreonactionmatchedandonenotconditionexpression)
- [IgnoreOn[Action]MatchedAndOneNotConditionNames](#ignoreonactionmatchedandonenotconditionnames)

## [Action]MatchedAnd

Use this option if you prefer to specify with an expression which properties you want to include.

```csharp
context.BulkMerge(customers, options => 
{
	// USE the code as the key expression
	options.ColumnPrimaryKeyExpression = x => x.Code;
	
	// ON UPDATE, modify customers only that has the same `IsLocked` value (always 0 on the source)
	options.MergeMatchedAndConditionExpression = x => new { x.Code, x.Name };
});
```

| Method 		  | Name                                     	   | Try it |
|:----------------|:-----------------------------------------------|--------|
| BulkMerge 	  | MergeMatchedAndOneNotConditionExpression 	   | [Fiddle](https://dotnetfiddle.net/LQZuak) |
| BulkUpdate 	  | UpdateMatchedAndOneNotConditionExpression	   | [Fiddle](https://dotnetfiddle.net/noelqT) |
| BulkSynchronize | SynchronizeMatchedAndOneNotConditionExpression | [Fiddle](https://dotnetfiddle.net/F7nbwA) |

## [Action]MatchedAndConditionNames

Use this option if you prefer to specify a list of properties names you want to include. The value must correspond to the property name or the navigation name.

```csharp
context.BulkMerge(customers, options => 
{
	// USE the code as the key expression
	options.ColumnPrimaryKeyExpression = x => x.Code;
	
	// ON UPDATE, modify customers only that has the same `IsLocked` value (always 0 on the source)
	options.MergeMatchedAndConditionNames = new List<string>() { nameof(Customer.Code), nameof(Customer.Name) };
});
```

| Method 		  | Name                                      | Try it |
|:----------------|:------------------------------------------|--------|
| BulkMerge 	  | MergeMatchedAndOneNotConditionNames		  | [Fiddle](#) |
| BulkUpdate 	  | UpdateMatchedAndOneNotConditionNames  	  | [Fiddle](#) |
| BulkSynchronize | SynchronizeMatchedAndOneNotConditionNames | [Fiddle](#) |

## IgnoreOn[Action]MatchedAndConditionExpression

Use this option if you prefer to specify with an expression which properties you want to exclude/ignore. All non-specified properties will be included.

```csharp
context.BulkMerge(customers, options => 
{
	// USE the code as the key expression
	options.ColumnPrimaryKeyExpression = x => x.Code;
	
	// ON UPDATE, modify customers only that has the same `IsLocked` value by excluding all other properties (always 0 on the source)
	options.IgnoreOnMergeMatchedAndConditionExpression = x => new { x.Note };
});
```

| Method 		  | Name                                       		 	   | Try it |
|:----------------|:-------------------------------------------------------|--------|
| BulkMerge 	  | IgnoreOnMergeMatchedAndOneNotConditionExpression 	   | [Fiddle](https://dotnetfiddle.net/XqgHKo) |
| BulkUpdate 	  | IgnoreOnUpdateMatchedAndOneNotConditionExpression  	   | [Fiddle](https://dotnetfiddle.net/65T8kP) |
| BulkSynchronize | IgnoreOnSynchronizeMatchedAndOneNotConditionExpression | [Fiddle](https://dotnetfiddle.net/zGSrJR) |

## IgnoreOn[Action]MatchedAndConditionNames

Use this option if you prefer to specify a list of properties names you want to exclude/ignore. The value must correspond to the property name or the navigation name. All non-specified properties will be included.

```csharp
context.BulkMerge(customers, options => 
{
	// USE the code as the key expression
	options.ColumnPrimaryKeyExpression = x => x.Code;
	
	// ON UPDATE, modify customers only that has the same `IsLocked` value by excluding all other properties (always 0 on the source)
	options.IgnoreOnMergeMatchedAndConditionNames = new List<string>() { nameof(Customer.Note) };
});
```

| Method 		  | Name                                       		  | Try it |
|:----------------|:--------------------------------------------------|--------|
| BulkMerge 	  | IgnoreOnMergeMatchedAndOneNotConditionNames		  | [Fiddle](#) |
| BulkUpdate 	  | IgnoreOnUpdateMatchedAndOneNotConditionNames  	  | [Fiddle](#) |
| BulkSynchronize | IgnoreOnSynchronizeMatchedAndOneNotConditionNames | [Fiddle](#) |


## Related Solutions

- [Matched and one not (Coming Soon)](#coming-soon)
- [MatchedAndFormula (Coming Soon)](#coming-soon)