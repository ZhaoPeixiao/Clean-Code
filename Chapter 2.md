# 有意义的命名

## 2.2 名副其实

变量、函数或者类的名称应该回答：它为什么存在，做什么事情，应该怎么用。 需要注释出来的名称不是名副其实。

```java
// Bad
public List<int[]> getThem(){
    List<int[]> list1 = new ArrayList<int[]>();
    for(int[] x : theList){
        if(x[0] == 4){
            list1.add(x);
        }
    }
    return list1;
}

// Good
public List<Cell> getFlaggedCells(){
    List<Cell> flaggedCells = new ArrayList<Cell>();
    for(Cell cell : gameBoard){
        if(cell.isFlagged()){
            flaggedCells.add(cell);
        }
    }
    return flaggedCells;
}                    
```



## 2.3 避免误导

避免使用与本意相悖的词。

```java
hp, aix, sco ---- Unix/类Unix平台专有名称
accountList 会被误解为List类型，可用accountGroup/accounts
```

提防使用外形相似度高的名称， 用小写数字1和字母O作为变量名。



## 2.4 做有意义的区分

只是为满足编译器或者解释器的需要而写代码，就会制造麻烦。

```java
// Bad
public static void copyChars(char a1[], char a2[]){
    for(int i = 0; i < a1.length; i++){
        a2[i] = a1[i];
    }
}

// Good
public static void copyChars(char source[], char destination[]){
    for(int i = 0; i < source.length; i++){
        destination[i] = source[i];
    }
}
```

废话是另一种没有意义的区分。 Product --- ProductInfo --- ProductData



## 2.5 使用读得出来的名称

```java
// Bad
class DtaRcrd012{
    private Data genymdhms;
    private Data modymdhms;
    private final String pszqint = "102";
}

// Good
class Customer{
    private Date generationTimestamp;
    private Date modificationTimestamp;
    private final String recordId = "102";
}
```



## 2.6 使用可搜索的名称

单字母名称仅用于短方法的本地变量，名称长短应与其作用域大小相对应。若变量或常量可能在代码中多处使用，则应赋予其便于搜索的名称。

```java
// Bad
for(int j = 0; j < 34; j++){
	s += (t[j]*4)/5;
}

// Good
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for(int j = 0; i < NUMBER_OF_TASKS; j++){
	int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
	int realTaskWeeks = realTaskDays / WORK_DAYS_PER_WEEK;
	sum += realTaskWeeks;
}
```



## 2.7 避免使用编码

### 2.7.1 匈牙利语标记法

增加了修改变量、函数或者类名称或者类型的难度，增加了阅读代码的难度，知道了让编码系统误导读者的可能性。

### 2.7.2 成员前缀

不必使用 m_ 前缀来表明成员变量。 应当把类和函数做的足够小，以消除对成员前缀的需要。

### 2.7.3 接口和实现



## 2.8 避免思维映射

不应当让读者在脑中把你的名称翻译为他们熟知的名称。 

明确是王道。



## 2.9 类名

类名和对象名应该是名词或者名词短语。



## 2.10 方法名

方法名应该是动词或动词短语。



## 2.11 别抖机灵

言到意到，意到言到。



## 2.12 每个概念对应一个词

给每个抽象概念一个词，并且一以贯之。



## 2.13 别用双关语

避免将同一单词用于不同目的。



## 2.14 使用解决方案领域名称

只有程序员会读你的代码，使用CS属于、算法名、模式名、数学术语。



## 2.15 使用源自所涉问题领域的名称





## 2.16 添加有意义的语境

用命名良好的类、函数或者名称空间来放置名称，给读者提供语境。

```java
// Bad
private void printGuessStatistics(char candidate, int count){
	String name;
    String verb;
    String pluralModifier;
    if(count == 0){
        number = "no";
        verb = "are";
        pluralModifier = "s";
    }else if(count == 1){
        number = "1";
        verb = "is";
        pluralModifier = "";
    }else{
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
    String guessMessage = String.format(
    "There %s %s 5s%s", verb, number, candidate, pluralModifier);
    print(guessMessage);
}

// Good
public class GuessStatisticsMessage{
	private String name;
    private String verb;
    private String pluralModifier;
    
    public String make(char candidate, int count) {
        createPluralDependentMessageparts(count);
        return String.format("There %s %s 5s%s", verb, number, candidate, pluralModifier);
    }
    
    private void createPluralDependentMessageparts(int count){
        if(count == 0){
            thereAreNoLetters();
        }else if(count == 1){
            ThereIsOneLetter();
        }else{
            ThereAreManyLetters();
        }
    }
    
    private void thereAreManyLetters(){
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
    
    private void ThereIsOneLetter(){
        number = "1";
        verb = "is";
        pluralModifier = "";
    }
    
    private void thereAreNoLetters(){
        number = "no";
        verb = "are";
        pluralModifier = "s";
    }
}
```



## 2.17 不要添加没用的语境

只要短名称足够清楚，就比长名称摇号。别给名称添加不必要的语境。