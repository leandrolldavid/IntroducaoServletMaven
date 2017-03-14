# Introducao a Servlets usando Maven

Apache Maven, ou Maven, é uma ferramenta de automação de compilação utilizada primariamente em projetos Java.
Vamos usar o maven para construir nossos projetos.

Para criar um projeto de servlet baseado em maven siga os seguintes passos:

1) Crie uma estrutura de arquivos da seguinte forma
```
├── Nome do projeto/
│   ├── pom.xml
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   ├── pacote
│   │   │   │   │   ├── MinhaServlet.java
│   │   │   ├── webapp
│   │   │   │   ├── WEB-INF
│   │   │   │   │   ├── web.xml
```
2) Insira o conteudo abaixo no pom.xml
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>net.javatutorial.tutorials</groupId>
	<artifactId>MinhaServlet</artifactId>
	<version>1</version>
	<packaging>war</packaging>

	
	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<dependencies>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>3.1.0</version>
			<scope>provided</scope>
		</dependency>
	</dependencies>

	<build>
		<sourceDirectory>src/main/java</sourceDirectory>

		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-war-plugin</artifactId>
				<version>2.3</version>
				<configuration>
					<warSourceDirectory>src/main/webapp</warSourceDirectory>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.1</version>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
				</configuration>
			</plugin>
		</plugins>
	</build>
</project>
```
3) Crie normalmente sua classe implementaço da servlet e seu web.xml. Nenhuma alteração em função do maven é necessária aqui.

4) Para gerar o war basta executar o comando abaixo:
```bash
mvn package
```
Ele ira fazer com que o maven baixe as dependencias e compile seu codigo. se tudo estiver ok ele gerará seu war na pasta target.

5) Uma maneira bastante simples de executar sua aplicação é usando um conteiner tomcat por meio do proprio maven. para isso, adicione o plug in abaixo no seu pom:
```xml
<plugin>
			  <groupId>org.apache.tomcat.maven</groupId>
			  <artifactId>tomcat7-maven-plugin</artifactId>
			  <version>2.1</version>
			  <configuration>
			    <path>/</path>
			  </configuration>
</plugin>
```
E execute o comando a seguir:
```bash
mvn clean install tomcat7:run
```
