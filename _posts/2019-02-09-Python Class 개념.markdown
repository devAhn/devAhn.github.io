---
layout: post
title:  "Python Class 개념(keep updating)"
date:   2019-02-09 02:13:09
author: 안상우
categories: Devlog
cover:  "/assets/pyhon.jpg"
---

클래스의 개념이 약하니 PyQt 를 사용할 때 힘들어 관련 내용을 복습하고 정리해보기로 하였다!

1. class 는 자료형 type


{% highlight python %}
class Human():
    '''사람'''
    def create(name,weight):
        person=Human()
        person.name=name
        person.weight=weight
        return person
    def eat(self):
        self.weight+=0.1
        print("{}가 먹어서 {}kg이 되었습니다.".format(person.name,person.weight))

    def walk(self):
        self.weight-=0.1
        print("{}가 걸어서 {}kg가 되었습니다.".format(person.name,person.weight))
    
    def speak(self,message):
        print(message)
{% endhighlight %}

클래스는 str이나 int 와 같은 자료형을 말한다. 내가 클래스를 만들어주고 관련 함수를 편하게 쓰려고 내장 시켜주는게 "method" 이다. 
메소드 : 클래스안 에 있는 함수
메소드 : 클래스에 묶여서 클래스의 인스턴스와 관계되는 일을 하는 함수

{% highlight python %}
class Human():
    '''인간'''
    def __init__(self, name, weight):
        '''초기화 함수'''
        self.name=name
        self.weight=weight
        
    def __str__(self):
        '''문자열화 함수'''
        return "{}(몸무게 {}kg)".format(self.name,self.weight)
    def eat(self):
        self.weight+=0.1
        print("{}가 먹어서 {}kg이 되었습니다.".format(person.name,person.weight))
   
{% endhighlight %}

대부분의 클래스는 __init__ 을 통해 인스턴스를 만들어준다. 
"초기화"라고도 한다. 매번 같은 기능을 공유하는 
새로운 객체를 만들어준다는 의미인것 같다. 
여기서 인스턴스란? 클래스의 종류에 속하는 개별 객체를 말한다. 
흔히들 비유하는 붕어빨 틀로 찍어낸 조금씩 다른 붕어빵 하나하나가 틀이란
클래스의 인스턴스이다. 조금 더 정확한 비유로 말하면 인간 클래스의 
철수, 민희, 민지 같은 인스턴스들이 있을 수 있다. 

또한 클래스 밑에 있는 함수, 즉 메소드들은 모두 첫번쨰 parameter로 self를 자동으로 갖는다.
안써있다고 하더라도 생략되있는 것뿐 모두 갖고 있다.

{% highlight python %}
#   __init__ 초기화 함수 : 인스턴스를 만들 때 실행되는 함수
#   __str__  문자열화 함수: 인스턴스 자체를 출력할 때의 형식을 지정해주는 함수
{% endhighlight %}


그런데! 다음과 같이 세 개의 클래스가 있다고 가정해보자 Animal, Cow, Dog
이런 경우에 Animal 클래스 하나가 Cow 와 Dog 클래스 두 개의 상위 그룹일 것이다.
동물은 먹으니 "먹는다"는 애니멀의 Method를 Cow와 Dog이 공유할 것이다. 이렇게 클래스가 다른
클래스에게 메소드를 전해주는 것을 "상속" 이라고 한다. 

{% highlight python %}

class Animal():
    
    def walk(self):
        print("걷는다")
        
    def eat(self):
        print("먹는다")
    
    def greet(self):
        print("인사한다.")

        
class Cow(Animal):
    '''소'''
    
class Human(Animal):
     
    def wave(self):
        print("손을 흔든다.")
        
    def greet(self):
        self.wave()
        
class Dog(Animal):
    
    def wag(self):
        print("꼬리를 흔든다")
        
    def greet(self):
        self.wag()
        
        
# 상속(inherit) 부모가 자식들에게 메소드를 똑같이 쓰게 물려줄 수 있다. 
# 동물 -> 사람, 개
# Override : 자식 클래스는 부모의 것을 상속받지만 똑같은 메소드를 만듦으로서 덮어쓸수 있다.

{% endhighlight %}

그런데 부모의 여러 함수를 상속받았느데 특정 함수는 자식만의 것으로 바꾸고 싶다면 어떻게 해야할까?
이럴 때 사용하는 것이 Override 오버라이드 이다. 

{% highlight python %}
class Animal():
    
    def walk(self):
        print("걷는다")
        
    def eat(self):
        print("먹는다")
    
    def greet(self):
        print("인사한다.")

        
class Cow(Animal):
    '''소'''
class Human(Animal):
     
    def wave(self):
        print("손을 흔든다.")
        
    def greet(self):
        self.wave()
        
class Dog(Animal):
    
    def wag(self):
        print("꼬리를 흔든다")
        
    def greet(self):
        self.wag()
        
        #위와 같이 그냥 덧붙여 사용해주면 된다.
        
{% endhighlight %}

세상에는 다양한 사람과 다양한 경우가 있다.
한 단계 더 나아가서 생각해보자. 오버라이드를 했는데 특정 패러미터,
혹 특정 함수는 부모의 것을 쓰고 싶을 때는 어떡할까? 
super().원하는메소드(패러미터) 로 처리하면 된다.
다음 코드에서 보여주겠다.
{% highlight python %}

#부모의 동작은 그대로 하면서 동작을 끼 어넣어?
class Animal():
    
    def __init__ (self, name): # 대부분의 클래스가 갖고 있는 초기화
        self.name= name
        
    def walk(self):
        print("걷는다")
        
    def eat(self):
        print("먹는다")
    
    def greet(self):
        print("{}이/가 인사한다.".format(self.name))

class Human(Animal):

    def __init__(self,name,hand):
        super().__init__(name) # name과 관련된 것은 부모가 처리하게 해준다. 
        self.hand= hand

    def wave(self):
        print("{}을 흔들면서".format(self.hand ))
        
        
    def greet(self):
        self.wave()
        super().greet()
        

{% endhighlight %}

아직 Class에 대한 내용이 완벽히 정리가 되지는 않았지만 그래도
대충 체계는 잡힌 거 같다. 
더 많은 분들의 생각과 의견을 찾아보고, 실습을 해보며 굳혀야 겠다.
