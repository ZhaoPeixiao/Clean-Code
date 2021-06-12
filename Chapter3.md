# 函数

## 3.1 短小

if else while语句等，代码块应该只占据一行，该行大抵应该是一个函数调用语句。



## 3.2 只做一件事

函数应该做一件事，做好这件事，只做这一件事。



## 3.3 每个函数一个抽象层级

要确保函数只做一件事，函数中的语句就要在同一抽象层级上。

自顶向下读代码：向下规则。 每个函数后面都跟着位于下一抽象层级的函数。



## 3.4 Switch语句

利用多态来实现。

```java
// Bad
public Money calculatePay(Employee e) throws InvalidEmployeeType{
    switch(e.type){
        case COMMISSIONED:
            return calculateCommissionedPay(e);
        case HOURLY:
            return calculateHourlyPay(e);
        case SALARIED:
			return calculateSalariedPay(e);
        default:
            throw new InvalidEmployeeType(e.type);
    }
}

// Good
public abstract class Employee{
    public abstract boolean isPayDay();
    public abstract Money calculatePay();
    public abstract void deliveryPay(Money pay);
}

public interface EmployeeFactory{
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}

public class EmployeeFactoryImpl implements EmployeeFactory{
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType{
        switch(r.type){
            case COMMISSIONED:
            	return CommissionedEmployee(r);
        	case HOURLY:
            	return HourlyEmployee(r);
        	case SALARIED:
				return SalariedEmployee(r);
        	default:
            	throw new InvalidEmployeeType(r.type);   
        }
    }
}
```



## 3.5 使用具有描述性的名称



## 3.6 函数参数

应尽量避免三函数参数，有足够特殊的理由才能使用三个以上的参数。

### 3.6.1 单参数函数的普遍形式

### 3.6.2 标识参数

### 3.6.3 双参数函数

### 3.6.4 三参数函数

### 3.6.5 参数对象

如果函数看起来需要三个或三个以上的参数，说明其中一些应该封装为类。

### 3.6.6 参数列表

### 3.6.7 动词与关键字

给函数取一个好名字，能较好地解释函数的意图，以及参数的顺序和意图。



## 3.7 无副作用



## 3.8 分割指令和询问



## 3.9 使用异常替代返回错误代码

```java
// Bad
if(deletePage(page) == E_OK){
    if(registry.deleteReference(page.name) == E_OK){
        if(configKeys.deleteKey(page.name.makeKey()) == E_OK){
			logger.log("page deleted");
        } else{
            logger.log("configKey not deleted");
        }
    } else{
        logger.log("deleteReference from registry falied");
    }
} else{
    logger.log("deletefalied");
    return E_ERROR;
}

// Good
try{
	deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
}
catch(Exception e){
    logger.log(e.getMessage());
}
```



## 3.10 别重复自己



## 3.11 结构化编程