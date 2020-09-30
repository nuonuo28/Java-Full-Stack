#### Sort Arraylist of String Using Collections

```java
import java.util.*;

public class Coding1 {
	public static void main(String[] args) {
		ArrayList<String> list = new ArrayList<>();
		list.add("A");
		list.add("g");
		list.add("c");
		list.add("L");
		list.add("f");
		list.add("1");
		System.out.println("Unsorted list: " + list);

		Collections.sort(list);
        // Collections.sort(list, Collections.reverseOrder()); 
		// Ascending order
		System.out.println("Sorted list: " + list);
	}
}
```

#### Find an Element in the Arraylist of String

```java
import java.util.*;

public class Coding1 {
	public static void main(String[] args) {
		ArrayList<String> list = new ArrayList<>();
		list.add("Dog");
		list.add("Cat");
		list.add("Bird");
		list.add("fish");

		if (list.contains("Dog")){
			System.out.println("Element found");
		} else {
			System.out.println("No such element");
		}

	}
}
```

#### Add Element in ArrayList in specific index

```java
import java.util.*;

public class Coding1 {
	public static void main(String[] args) {
		List<String> list = new ArrayList<>();
		list.add("Dog");
		list.add("Cat");
		list.add("Bird");
		list.add("fish");

		System.out.println(list);
		list.add(0, "Monkey");
		System.out.println(list);
	}
}
```

#### Replace Element in ArrayList in specific index

```java
import java.util.*;

public class Coding1 {
	public static void main(String[] args) {
		List<String> list = new ArrayList<>();
		list.add("Dog");
		list.add("Cat");
		list.add("Bird");
		list.add("fish");

		System.out.println(list);
		list.set(1, "Kitty");
		System.out.println(list);
	}
}
```

#### HashSet to Array

```java
import java.util.*;
public class Coding1 {
	public static void main(String[] args) {
		Set<Integer> set = new HashSet<>();
		set.add(12);
		set.add(23);
		set.add(5);
		set.add(16);

		System.out.println("Hash Set: " + set);

		Object[] obj = set.toArray();
		for (Object o : obj) {
			System.out.println(o);
		}
	}
}
```

#### Remove Element from LinkedHashSet

```java
import java.util.*;
public class Coding1 {
	public static void main(String[] args) {
		LinkedHashSet<String> linked = new LinkedHashSet<>();
		linked.add("e1");
		linked.add("e2");
		linked.add("e3");

		System.out.println("Linked Hash Set: " + linked);

		linked.remove("e2");
		System.out.println("Linked Hash Set: " + linked);
	}
}
```

#### Reverse Elements of a Stream in Java

```java
import java.util.*;
import java.util.stream.Collector;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Coding1 {
	public static void main(String[] args) {
		Stream<Integer> stream = Stream.of(1,2,3,4,5);
		Stream<Integer> reverse = stream.collect(reverse());
		reverse.forEach(System.out::println);
	}

	public static <T> Collector<T, ?, Stream<T>> reverse() {
		return Collectors.collectingAndThen(Collectors.toList(), list -> {
			Collections.reverse(list);
			return list.stream();
		});
	}
}
```

#### TreeSet to Integer Array

```java
import java.util.*;

public class Coding1 {
	public static void main(String[] args) {
		TreeSet<Integer> set = new TreeSet<>();
		set.add(1);
		set.add(2);
		set.add(3);

		Integer[] res = set.toArray(new Integer[set.size()]);
		for (Integer i : res) {
			System.out.println(i);
		}
	}
}
```

#### Map to Stream

```java
import java.util.*;
import java.util.stream.*;

public class Coding1 {
	public static void main(String[] args) {
		Map<Integer, String> map = new HashMap<>();
		map.put(1, "a");
		map.put(2, "b");
		map.put(3, "c");
		System.out.println("Map: " + map);

		Stream<Map.Entry<Integer, String>> stream = mapToStream(map);
		System.out.println(Arrays.toString(stream.toArray()));

	}

	public static <K,V> Stream<Map.Entry<K,V>> mapToStream (Map<K, V> map) {
		return map.entrySet().stream();
	}
}
```

#### Sort the object using Stream

```java
import java.util.*;

public class Coding1 {
	public static void main(String[] args) {
		List<User> userList = new ArrayList<>();
		userList.add(new User("a", 18));
		userList.add(new User("b", 20));
		userList.add(new User("c", 12));

		User minAge = userList.stream().min(Comparator.comparingInt(User::getAge)).get();
		System.out.println(minAge);

		User maxAge = userList.stream().max(Comparator.comparingInt(User::getAge)).get();
		System.out.println(maxAge);
	}
}

class User {
	private String name;
	private Integer age;

	public User(String name, Integer age) {
		this.name = name;
		this.age = age;
	}

	public Integer getAge () {
		return age;
	}

	@Override
	public String toString() {
		return "Name: " + name + ", Age: " + String.valueOf(age); 
	}

}
```

