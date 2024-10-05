# Implement Design Pattern

## Singleton Pattern

- Trong Spring Boot, các annotation phổ biến như `@Component, @Bean, @Controller, @Service, @Repository, @Slf4j...` , ngoài ra cũng có `enum, LoggerFactory,...` **đều mặc định sử dụng Singleton Pattern**. Điều này có nghĩa là Spring sẽ chỉ tạo một instance duy nhất cho mỗi bean và sử dụng lại đối tượng này xuyên suốt vòng đời của ứng dụng.

- Cách implement:

    ```java
    // Lazy Initialization
    class Singleton_1 {
        private String name;
        private int age;
        private static Singleton_1 instance;

        private Singleton_1(String name, int age) {
            this.name = name;
            this.age = age;
        }

        public static Singleton_1 getInstance(String name, int age) {
            if (Objects.isNull(instance)) {
                instance = new Singleton_1(name, age);
            }

            return instance;
        }

        @Override
        public String toString() {
            return "Singleton_1{name='" + name + '\'' + ", age=" + age + '}';
        }
    }

    // Enum Singleton
    enum Singleton_2 {
        INSTANCE("An", 23);

        private String name;
        private int age;

        Singleton_2(String name, int age) {
            this.name = name;
            this.age = age;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public int getAge() {
            return age;
        }

        public void setAge(int age) {
            this.age = age;
        }

        @Override
        public String toString() {
            return "Singleton_2{name='" + name + '\'' + ", age=" + age + '}';
        }
    }
    ```

## Builder Pattern

- Loại này hay được dùng trong `@Builder của lombok, StringBuilder, HttpClient, HttpRequest, Calendar, Locale,...`

- Cách implement:

    ```java
    class Scratch {
        public static void main(String[] args) {
            Person person = Person.builder()
                    .name("An")
                    .age(23)
                    .gender(Gender.MALE)
                    .phoneNumber("1234567890")
                    .address("Thuong Tin")
                    .email("abc@gmail.com")
                    .company("IntrustCA")
                    .position("Employee")
                    .build();
            System.out.println(person);
        }
    }

    class Person {
        private String name;
        private int age;
        private Gender gender;
        private String phoneNumber;
        private String address;
        private String email;
        private String company;
        private String position;
        
        public Person(String name, int age, Gender gender, String phoneNumber, String address, String email, String company, String position) {
            this.name = name;
            this.age = age;
            this.gender = gender;
            this.phoneNumber = phoneNumber;
            this.address = address;
            this.email = email;
            this.company = company;
            this.position = position;
        }

        public static PersonBuilder builder() {
            return new PersonBuilderImpl();
        }

        @Override
        public String toString() {
            return "Person{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    ", gender=" + gender +
                    ", phoneNumber='" + phoneNumber + '\'' +
                    ", address='" + address + '\'' +
                    ", email='" + email + '\'' +
                    ", company='" + company + '\'' +
                    ", position='" + position + '\'' +
                    '}';
        }
    }

    enum Gender {
        MALE, FEMALE
    }

    interface PersonBuilder {
        PersonBuilder name(String name);

        PersonBuilder age(int age);

        PersonBuilder gender(Gender gender);

        PersonBuilder phoneNumber(String phoneNumber);

        PersonBuilder address(String address);

        PersonBuilder email(String email);

        PersonBuilder company(String company);

        PersonBuilder position(String position);

        Person build();
    }

    class PersonBuilderImpl implements PersonBuilder {
        private String name;
        private int age;
        private Gender gender;
        private String phoneNumber;
        private String address;
        private String email;
        private String company;
        private String position;

        @Override
        public PersonBuilder name(String name) {
            this.name = name;
            return this;
        }

        @Override
        public PersonBuilder age(int age) {
            this.age = age;
            return this;
        }

        @Override
        public PersonBuilder gender(Gender gender) {
            this.gender = gender;
            return this;
        }

        @Override
        public PersonBuilder phoneNumber(String phoneNumber) {
            this.phoneNumber = phoneNumber;
            return this;
        }

        @Override
        public PersonBuilder address(String address) {
            this.address = address;
            return this;
        }

        @Override
        public PersonBuilder email(String email) {
            this.email = email;
            return this;
        }

        @Override
        public PersonBuilder company(String company) {
            this.company = company;
            return this;
        }

        @Override
        public PersonBuilder position(String position) {
            this.position = position;
            return this;
        }

        @Override
        public Person build() {
            return new Person(name, age, gender, phoneNumber, address, email, company, position);
        }
    }
    ```

## Factory pattern

- Spring cũng áp dụng Factory Pattern để quản lý quá trình tạo và quản lý bean(`@Component, @Bean, @Controller, @Service, @Repository,...`)

- Cách implement:

    ```java

    ```
