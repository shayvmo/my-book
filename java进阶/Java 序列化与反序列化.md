### Java 序列化与反序列化

> 序列化在计算机科学的数据处理中，是指将数据结构或对象状态转换成可取用格式，以留待后续在相同或另一台计算机环境中，能恢复原先状态的过程。依照序列化格式重新获取字节的结果时，可以利用它来产生与原始对象相同语义的副本。

最近更新：2020年12月14日



序列化（`serialize`）：对象   ->  字节流 

反序列化（`deserialize`）：字节流  -> 对象



#### 序列化作用

- **序列化可以将对象的字节序列存持久化**：可以将其保存在内存、文件、数据库中（见下图）；
- **可以在网络上传输对象字节序列**；
- **可用于远端程序方法调用**



#### 实现序列化

- `ObjectOutputStream`类下的`void writeObject(Object obj)`方法用于将一个对象写入对象输出流，也就是序列化；
- `ObjectInputStream`类下的`Object readObject()`方法用于读取一个对象到输入流，也就是反序列化



```java
import java.io.*;

public class SerializeDemo1 {

    static class Cat implements Serializable {
        private static final long serialVersionUID = 1L;

        private String nickname;

        private Integer age;

        public Cat() {}

        public Cat(String nickname, Integer age) {
            this.nickname = nickname;
            this.age = age;
        }

        @Override
        public String toString() {
            return "Cat{" +
                    "nickname='" + nickname + '\'' +
                    ", age=" + age +
                    '}';
        }
    }

    /**
     * 序列化方法
     * @param filepath 文件路径
     * @param cat 要序列化的对象
     * @throws IOException
     */
    private static void serialize(String filepath, Cat cat) throws IOException {
        // 实例化file对象
        File file = new File(filepath);
        // 实例化文件输出流
        FileOutputStream fileOutputStream = new FileOutputStream(file);
        // 实例化对象输出流
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
        // 保存cat对象
        objectOutputStream.writeObject(cat);
        // 关闭流
        fileOutputStream.close();
        objectOutputStream.close();
    }

    /**
     * 反序列化方法
     * @param filepath 文件路径
     * @throws IOException
     * @throws ClassNotFoundException
     */
    private static void deserialize(String filepath) throws IOException, ClassNotFoundException {
        // 实例化file对象
        File file = new File(filepath);
        // 实例化文件输入流
        FileInputStream fileInputStream = new FileInputStream(file);
        // 实例化对象输入流
        ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
        Object o = objectInputStream.readObject();
        System.out.println(o);
    }

    public static void main(String[] args) throws IOException, ClassNotFoundException {
        String filename = "C:\\Users\\Colorful\\Desktop\\imooc\\Hello.txt";
        Cat cat = new Cat("猪皮", 1);
        serialize(filename, cat);
        deserialize(filename);
    }

}

```





#### Seralizable 接口

被序列化的类必须是`Enum`、`Array`或`Serializable`中的任意一种类型

如果要序列化的类不是枚举类型和数组类型的话，则必须实现`java.io.Seralizable`接口，否则直接序列化将抛出`NotSerializableException`异常



- ### serialVersionUID

  - `serialVersionUID` 是 Java 为每个序列化类产生的版本标识

- ### 默认序列化机制

  - 如果仅仅只是让某个类实现 `Serializable` 接口，而没有其它任何处理的话，那么就会使用默认序列化机制

- ### transient 关键字

  - 在现实应用中，有些时候不能使用默认序列化机制





#### 常用序列化工具

- [thrift](https://github.com/apache/thrift)、[protobuf](https://github.com/protocolbuffers/protobuf) - 适用于对性能敏感，对开发体验要求不高的内部系统。
- [hessian](http://hessian.caucho.com/doc/hessian-overview.xtp) - 适用于对开发体验敏感，性能有要求的内外部系统。
- [jackson](https://github.com/FasterXML/jackson)、[gson](https://github.com/google/gson)、[fastjson](https://github.com/alibaba/fastjson) - 适用于对序列化后的数据要求有良好的可读性（转为 json 、xml 形式）。





































