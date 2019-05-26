# Day1

## 开始一个项目

今天的练习题目是FizzBuzz。

在`IntelliJ IDEA`里新建一个`gradle`项目，在`build.gradle`里引入`spock`，最终内容如下：

```groovy
group 'learn-tdd'
version '1.0-SNAPSHOT'

apply plugin: 'java'

sourceCompatibility = 1.8

repositories {
    mavenCentral()
}

dependencies {
    testCompile group: 'org.spockframework', name: 'spock-core', version: '1.3-groovy-2.5'
}
```

这样就可以开始了。

## 最终结果

测试：

```groovy
package tdd.sample

import spock.lang.Specification

class FizzBuzzGameTest extends Specification {
    FizzBuzzGame game

    void setup() {
        game = new FizzBuzzGame()
    }

    def "convert a number to greet world"() {
        expect:
        result == game.convert(n)

        where:
        n   |   result
        1   |   "1"
        2   |   "2"
        3   |   "Fizz"
        5   |   "Buzz"
        15  |   "FizzBuzz"
        13  |   "Fizz"
        52  |   "Buzz"
        35  |   "Fizz" //应该这样吗？还是FizzBuzz？
        100 |   "Buzz"

    }
}
```

代码：

```java
package tdd.sample;

public class FizzBuzzGame {
    public String convert(int n) {
        Num num = new Num(n);
        if(num.isMultipleOf(3, 5)) return "FizzBuzz";
        if(num.isRelatedTo(3)) return "Fizz";
        if(num.isRelatedTo(5)) return "Buzz";
        return n+"";
    }

    static class Num {
        private final int n;

        Num(int n){this.n = n;}

        boolean isRelatedTo(int i) {
            return n % i == 0 || String.valueOf(n).contains(i+"");
        }

        boolean isMultipleOf(int i, int j) {
            return n % i == 0 && n % j ==0;
        }
    }
}
```



总结：

- 打字输入太不熟练，影响思路的连贯性。后续需要练习打字 https://typing.io/
- 需求中没有`Multiple`，`RealteTo`这样的概念，我觉得这样抽象一下更简洁。@小波老西 的意思是尽量不要出现需求中没有的概念和词汇。想想还是很有道理，如果实际工作中，应该推动产品经理去改需求文档，需求文档中用这样的概念表述，代码里再这样写——这样才有可能实现 "统一的语言"；



# Day2

## 键盘

今天的任务时"清理桌面"，即提升编码的速度。

昨天没有带外接键盘，今天接上了我的`FLICO MINILA`，并且利用IDEA的`Live Template`功能来加速输入。把`FizzBuzz`再撸了一遍，跑通第一个测试用例用例1分12秒。

我的键盘设置是把`cmd`和`Capslock`两个键互换的，在Mac上很多快捷键按起来会舒服些，另外，`FLICO MINILA`的Fn键很有用，右手大拇指按住Fn，左手E/D/S/F键可以控制光标上/下/左/右，这样，输入时控制光标两手几乎不用动地方。这样就可以做的避免使用鼠标了。

## Live Template

常用的代码块可以配置成`Live Template`，今天，把spock的`expect...where`做成了Live Template：

```groovy
def "$testname$"() {
    expect:
    result == $testmethod$($p0$)
    
    where:
    $p0$    |   result
    $p1$    |   $r1$
}
```

> 别名我用了 spexpect，上下文设置成 groovy

## 快捷键

今天用到的快捷键：

- `Cmd` + `N`
- `Ctrl` + `Option` + `R`
- `Ctrl` + `R`
- `Cmd` + `Shift` + `T`