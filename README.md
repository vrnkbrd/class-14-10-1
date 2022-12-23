# class-14-10-1
### Task 8kyu
Consider an array/list of sheep where some sheep may be missing from their place. We need a function that counts the number of sheep present in the array (true means present).
### My solution: 
```Java
public class Counter {
  public int countSheeps(Boolean[] arrayOfSheeps) {
    int sheep = 0;
    int x = 0;
    int len = arrayOfSheeps.length;
    while (x < len) {
        if (arrayOfSheeps[x] == true) sheep++;    
        x++;
    }
   return sheep;
  }
}
```

### Fav solution: 
```Java
import java.util.Arrays;
import java.util.function.Predicate;
public class Counter {
  public int countSheeps(Boolean[] arrayOfSheeps) {
    return (int) Arrays.stream(arrayOfSheeps).filter(Predicate.isEqual(Boolean.TRUE)).count();
  }
}
```
I loved that the participant used predicates and it was able to writh the whole code in one libe without any exceptions. 

### Task 6 kyu 
Given a list and a number, create a new list that contains each number of list at most N times, without reordering.
For example if the input number is 2, and the input list is [1,2,3,1,2,1,2,3], you take [1,2,3,1,2], drop the next [1,2] since this would lead to 1 and 2 being in the result 3 times, and then take 3, which leads to [1,2,3,1,2,3].
With list [20,37,20,21] and number 1, the result would be [20,37,21].

My solution: 
```Java
import java.util.*;

public class EnoughIsEnough {

  public static int[] deleteNth(int[] elements, int maxOcurrences) {
    if(maxOcurrences == 0) return new int[0];
    
    Map<Integer,Integer> map = new HashMap<>(elements.length);  
    LinkedList<Integer> retList = new LinkedList<Integer>();
    
    for(int i=0; i<elements.length; i++){
      int el = elements[i];
      Integer v = map.get(el);
      
      if(v != null){
        map.put(el, v+1);
        if(v+1 > maxOcurrences){ elements[i] = -1; } else { retList.add(el); }
      }else{
        map.put(el,1);
        retList.add(el);
      }
    }
    
    return retList.stream().mapToInt(i->i).toArray();
  }
}
```

Fav solution: 
```Java
import java.util.HashMap;
import java.util.Map;
import java.util.stream.IntStream;

public class EnoughIsEnough {
  public static int[] deleteNth(int[] elements, int maxOccurrences) {
    Map<Integer, Integer> occurrence = new HashMap<>();
    return IntStream.of(elements)
      .filter(motif -> occurrence.merge(motif, 1, Integer::sum) <= maxOccurrences)
      .toArray();
  }
}
```
