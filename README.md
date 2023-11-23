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
