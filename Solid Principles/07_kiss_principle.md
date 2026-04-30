# KISS Principle (keep it simple, stupid)

## One Liner
Favors simple, clear solution over complicated onces.
Simple code is easier to read, test and maintain.

# One Way
```java
public int sum(int[] arr){
    return Arrays.stream(arr).sum(); 
}
```

# Other Way
```java
public int sum(int[] arr){
    int total = 0;
    for(int num : arr){
        total += num;
    }
}
```

if (a>b) : For true : For false

Hard for user to read statement.

if()
{

}
else
{

    
}