# Word Ladder
## https://leetcode.com/problems/word-ladder

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list.

Note:

1. Return 0 if there is no such transformation sequence.
2. All words have the same length.
3. All words contain only lowercase alphabetic characters.
4. You may assume no duplicates in the word list.
5. You may assume beginWord and endWord are non-empty and are not the same.
```
Example 1:

Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.

Example 2:

Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

# Implementation :
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> set = new HashSet<>(wordList);
        if(!set.contains(endWord))
            return 0;
        
        Queue<String> q = new ArrayDeque<>();
        q.add(beginWord);
        Set<String> visited = new HashSet<>();
        visited.add(beginWord);
        
        int transformations = 1;
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i = 0; i < size; i++) {
                String word = q.poll();
                if(word.equals(endWord))
                    return transformations;
                
                for(int j = 0; j < word.length(); j++) {
                    for(int k = 'a'; k <= 'z'; k++) {
                        char[] chars = word.toCharArray();
                        chars[j] = (char) k;
                        String newStr = new String(chars);
                        if(set.contains(newStr) && !visited.contains(newStr)) {
                            q.add(newStr);
                            visited.add(newStr);
                        }
                    }
                }
            }
            transformations++;
        }
        return 0;
    }
}
```



# References :
https://www.youtube.com/watch?v=5iFZP-f40iI

