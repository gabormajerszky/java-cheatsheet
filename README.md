# Java Cheatsheet #
<br/>


How should my environment variables be set up?
-
You need to do 2 things:
1. Set the user variable JAVA_HOME to the JDK's root folder
2. Append the system variable Path with the the JDK's bin folder
<br/><br/><br/>


What order should my modifiers be in?
-
Google's style guide and the Java Language Specification recommends:
```
public protected private abstract default static final transient volatile synchronized native strictfp
```
<br/><br/>


How do I read a file?
-
There are many ways, but an easy one is this:
```
private static String readFileUtf(String pathString) throws IOException {
    byte[] bytes = Files.readAllBytes(Paths.get(pathString));
    return new String(bytes, StandardCharsets.UTF_8);
}
```
<br/><br/>


How do I convert a number to binary?
-
If it's an int:
```
Integer.toBinaryString(intValue)
```
If it's a long:
```
Long.toBinaryString(longValue)
```
<br/><br/>


How do I create an immutable list?
-
Using the guava libraries, you can do:
```
ImmutableList<Integer> immutableList = ImmutableList.of(1, 2, 3);
```
Using the builder:
```
ImmutableList<Integer> immutableList = new ImmutableList.Builder<Integer>()
        .add(1)
        .add(2)
        .add(3)
        .build();
```
<br/><br/>


How do I create an immutable map?
-
Using the guava libraries, for up to 5 keys, you can do:
```
ImmutableMap<String, Integer> immutableMap = ImmutableMap.of(
        "a", 1,
        "b", 2,
        "c", 3,
        "d", 4,
        "e", 5
);
```
Using the builder:
```
ImmutableMap<String, Integer> immutableMap = ImmutableMap.<String, Integer>builder()
        .putAll(mutableMap)
        .put("f", 6)
        .put("g", 7)
        .put("h", 8)
        .build();
```
<br/><br/>


How do I create an ordered map?
-
If you mean a map with a predictable iteration order, then either use ImmutableMap, or:
```
Map<String, Integer> map = new LinkedHashMap<>();
map.put("c", 3);
map.put("b", 2);
map.put("a", 1);    
```
<br/><br/>


How do I join a list of strings to a single string?
-
Simply use String's join function:
```
List<String> letters = Arrays.asList("a", "b", "c");
String joined = String.join(",", letters);
```
<br/><br/>


How do I join a list of integers or other objects to a single string?
-
Using streams:
```
List<Integer> numbers = Arrays.asList(1, 2, 3);
String joined = numbers.stream()
        .map(String::valueOf)
        .collect(Collectors.joining(","));
```
More concisely with guava:
```
List<Integer> numbers = Arrays.asList(1, 2, 3);
String joined = Joiner.on(",").join(numbers);
```
<br/><br/>


How do I convert an array of integers to a list?
-
If a fixed-size list will work, then:
```
Integer[] array = { 1, 2, 3 };
List<Integer> list = Arrays.asList(array);
```
If not, then with streams:
```
Integer[] array = { 1, 2, 3 };
List<Integer> list = Arrays.stream(array)
        .collect(Collectors.toList());
```
<br/><br/>


How do I convert an array of ints to a list?
-
Using streams and boxing:
```
int[] array = { 1, 2, 3 };
List<Integer> list = Arrays.stream(array)
        .boxed()
        .collect(Collectors.toList());
```
<br/><br/>


How do I test if an object can be properly serialized?
-
Using the SerializationUtils from the spring framework and Assert from junit:
```
byte[] serialized = SerializationUtils.serialize(original);
Object deserialized = SerializationUtils.deserialize(serialized);
Assert.assertEquals(original, deserialized);
```
<br/><br/>