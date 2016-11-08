# Coding

# public class Solution {
  List<Integer> allAnagrams(String s, String l) {
    // Write your solution here.
    List<Integer> result = new ArrayList<>();
    if (l.isEmpty()) {
      return result;
    }
    if (s.length() > l.length()) {
      return result;
    }
    // sliding window size of s
    Map<Character, Integer> map = countMap(s);
    int match = 0;
    // adding the new(rightmost) element at the current window
    for (int i = 0; i < l.length(); i++) {
      char temp = l.charAt(i);
      Integer count = map.get(temp);
      if (count != null) {
        map.put(temp, count - 1);
        if (count == 1) {
          match++;
        }
      }
    // removing the old(leftmost) element at the previous window
      if (i >= s.length()) {
        temp = l.charAt(i - s.length());
        count = map.get(temp);
        if (count != null) {
          map.put(temp, count + 1);
          if (count == 0) {
            match--;
          }
        }
      }
      // for the curent window, if all matched, count are all 0
      if (match == map.size()) {
        result.add(i - s.length() + 1);
      }
    }
    return result;
  }
  
  private Map<Character, Integer> countMap(String s) {
    Map<Character, Integer> map = new HashMap<>();
    for (char ch : s.toCharArray()) {
      Integer count = map.get(ch);
      if (count == null) {
        map.put(ch, 1);
      } else {
        map.put(ch, count + 1);
      }
    }
    return map;
  }
}
