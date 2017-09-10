It's a simple inline-hook framework works for intel(32bit,64bit) and arm(only works for arm32 and thumb) just now, and it's based on new c++11 feature.

<b>How to build</b>:
the framework based on cmake 2.8, all you have to do is:<br/>
cmake .</br>
make<br/>

<b>How to use</b>:<br/>
The usage of the this framework is very easy,example(main.cpp) shows below:<br/>

```c++

void print(const char *s) {
    std::cout << s << std::endl;
}

int my_strcmp(const char *s1, const char *s2) {
    std::cout << s1 << " " << s2 << ",haha, it's been hooked" << std::endl;
    return 0;
}

int main() {
    const char *s1 = "hello";
    const char *s2 = "world";

    using namespace hooker;
    HookerFactory* factory = HookerFactory::getInstance();
    const Hooker& hooker = factory->getHooker();
    hooker.hook(reinterpret_cast<void *>(strcmp), reinterpret_cast<void *>(my_strcmp), nullptr);

    if (strcmp(s1,s2) == 0) {
        print("equal");
    } else {
        print("not equal");
    }

    hooker.unhook(reinterpret_cast<void *>(strcmp));

    if (strcmp(s1,s2) == 0) {
        print("equal");
    } else {
        print("not equal");
    }

	delete factory;

    return 0;
}

```

The output is as below:
![image](imgs/crop.png)

