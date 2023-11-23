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

###105
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
