# Spring Boot

Criado pela Spring Source em 2012, com o intuito de facilitar todo o setup/configuração do Spring para projetos Java. Trabalha em conjunto com gerenciadores de dependências, como o Maven ou Gradle, para agilizar o preparo dos projetos.

Sem necessidade de criar arquivos de configuração. Ao adicionar uma dependência, é feita uma configuração inicial automática.

Execução simplificada: sem deploy em servidor externo.

![Spring Boot](https://i.imgur.com/74wKmfq.png)

[Criação de um projeto](http://start.spring.io)

Importar o projeto em uma IDE;

Criando um controller de demonstração (Hello World) que será executado ao acessar um diretório que foi mapeado ("/"):

```java
package com.dio.springboot.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/")
    public String helloMessage() {
        return "Hello, world!";
    }
}
```

Pode-se executar o projeto ao rodar uma task Maven, pela própria IDE, ou no terminal:

```
cd diretorio/projeto
mvn spring-boot:run
```

Ao acessar o *localhost:8080/*, será exibida a mensagem *"Hello, world!"* que foi especificada no HelloController. 

## FatJar/UberJar

Artefato do projeto pronto para execução;

Container Web embutido na geração e execução (Tomcat);

Deploy embarcado com outros containers são opcionais;

Dependências principais do projeto embarcadas.

![FatJar/UberJar](https://i.imgur.com/BKAdml5.png)

[Projeto no Github](https://github.com/rpeleias/springboot_digital_innovation_one)

## Referências

https://dzone.com/articles/spring-boot-framework-tutorials

https://www.javaavancado.com/o-que-e-spring-boot/

https://www.tutorialspoint.com/spring_boot/spring_boot_introduction.htm

https://docs.spring.io/spring-boot/docs/2.2.0.M5