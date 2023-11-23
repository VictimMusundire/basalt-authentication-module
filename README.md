# basalt-authentication-module

## Overview

## This is the runnable service for Basalt authentication

## Keycloak Setup using Docker
We run keycloak using Docker containers pointing to a DB
Create a database called *basalt_auth_db*
Start the container
Please check for the latest container build here: https://quay.io/repository/keycloak/keycloak
### Dev:
```shell
docker run --name basalt-keycloak-server --network host -d \
        -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=password \
        quay.io/keycloak/keycloak:21.0.1 \
        start-dev \
        --db=postgres \
        --features=token-exchange \
        --db-url=jdbc:postgresql://localhost/basalt_auth_db \
        --db-username=postgres \
        --db-password=postgres \
        --hostname-strict=false
```
### Ignore the below what what ....

### 105

Different compression techniques are used in order to reduce the size of the messages sent over the web. An algorithm is designed to compress a given string by describing the total number of consecutive occurences of each character next to it. For example, consider the string "abaasass". Group the consecutive occurence of each character:  'a' occurs one time, 'b' occurs one time, 'a' occurs two times consecutively, 's' occurs one time, 'a' occurs one time 's' occurs two times consecutively. If a character only occurs once, it is added to the compression string. If it occurs consecutive times the character is added to the string followed by an integer representing the number of consecutive occurrences, thus the compressed form of a string is "aba2sas2". Write a spring boot java function called compressedString, the function must return the compressed form of the message. compressedString method takes a string parameter called message and returns a compressed string message. 

@SpringBootApplication
public class SpringCertificationCodeApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringCertificationCodeApplication.class, args);
        System.out.println(compress("abaasass"));
    }

    private static String compress(String input) {
        if (input == null || input.isEmpty()) {
            return ""; // Handle empty or null input
        }

        StringBuilder compressed = new StringBuilder();
        int count = 1;

        for (int i = 1; i < input.length(); i++) {
            if (input.charAt(i) == input.charAt(i - 1)) {
                count++;
            } else {
                compressed.append(input.charAt(i - 1));
                if (count > 1) {
                    compressed.append(count);
                }
                count = 1;
            }
        }

        compressed.append(input.charAt(input.length() - 1));
        if (count > 1) {
            compressed.append(count);
        }

        return compressed.toString();
    }

}


---------------------------------------------------------------------------------------------

### 302

Given a set of words and a set of sentences(composed of those words), determine how many sentences can be created by rearranging the letters of each word in each input sentence, where rearranging words is only possible if the resulting word is also present in the input set of words. Example, wordSet = ['listen','silent','it','is'] , sentence = 'listen it is silent'. Note: The words in the set are unique, sentences are composed only of words from the word set and a sentence is composed of words separated by a single ' '. Determine that the letters of listen can be rearranged into silent (i.e these words are anagrams). Those two words can be replaced with each other. The four sentences that can be created are: listen it is silent, listen it is listen, silent it is silent, silent it is listen. Write a spring boot java function called countSentences that has string wordSet[n]:  an array of unique strings and string sentences[m]: an array of strings as parameters, it returns int[]: an array of m integers that denote the number of sentences that can be formed from each sentence.  


@SpringBootApplication
public class SpringCertificationCodeApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringCertificationCodeApplication.class, args);
        String[] wordSet = {"listen", "silent", "it", "is"};
        String[] sentences = {"listen it is silent", "listen it is listen", "silent it is silent", "silent it is listen"};

        System.out.println(Arrays.toString(countSentences(wordSet,sentences)));
    }

    public static int[] countSentences(String[] wordSet, String[] sentences) {

        int[] result = new int[sentences.length];

        // Build a map to store the frequency of each word in the wordSet
        Map<String, Integer> wordFrequencyMap = new HashMap<>();
        for (String word : wordSet) {
            wordFrequencyMap.put(word, wordFrequencyMap.getOrDefault(word, 0) + 1);
        }

        // Iterate through each sentence and count the valid sentences
        for (int i = 0; i < sentences.length; i++) {
            result[i] = countValidSentences(sentences[i], wordFrequencyMap);
        }

        return result;
    }

    private static int countValidSentences(String sentence, Map<String, Integer> wordFrequencyMap) {
        String[] words = sentence.split(" ");
        int validSentenceCount = 1;

        // Count the number of valid sentences that can be formed
        for (String word : words) {
            if (wordFrequencyMap.containsKey(word) && wordFrequencyMap.get(word) > 0) {
                wordFrequencyMap.put(word, wordFrequencyMap.get(word) - 1);
            } else {
                validSentenceCount = 0;
                break;
            }
        }

        // Restore the original word frequencies
        for (String word : words) {
            wordFrequencyMap.put(word, wordFrequencyMap.getOrDefault(word, 0) + 1);
        }

        return validSentenceCount;
    }

}
