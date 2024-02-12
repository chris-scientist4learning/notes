---
layout: default
title: "Gestion des logs - Hibernate"
permalink: /formation/hibernate/logs-manager/
lang: fr
my_menu: menu-hibernate.html
---

## Gestion des logs

Pour ajouter des logs lors de tests unitaires, il est nécessaire d'ajouter le fichier *logback-test.xml* suivant dans *src/test/resources/* :

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

	<appender name="STDOUT"
		class="ch.qos.logback.core.ConsoleAppender">
		<encoder>
			<pattern>
				%d{HH:mm:ss} %highlight(%-5level) %logger{15}.%M %msg%n
			</pattern>
		</encoder>
	</appender>
	
	<logger name="org.hibernate.SQL" level="DEBUG" />
	<logger name="org.hibernate.type.descriptor.sql.BasicBinder" level="TRACE" />
	<!-- Logs des transactions -->
    <logger name="org.springframework.orm.jpa.JpaTransactionManager" level="DEBUG" />
    <!-- Logs de session -->
	<logger name="org.hibernate.internal.SessionImpl" level="TRACE" />
	
	<root level="WARN">
		<appender-ref ref="STDOUT" />
	</root>

</configuration>
```

### Ajouter des logs spécifique

Il peut être nécessaire d'ajouter des logs spécifique à une classe comme nous allons le voir.

Voici un exemple :
```
package io.github.chrisscientist.hibernate.tutorial.repository;

import java.util.List;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Repository;

import io.github.chrisscientist.hibernate.tutorial.domain.Movie;
import jakarta.persistence.EntityManager;
import jakarta.persistence.PersistenceContext;

import org.springframework.transaction.annotation.Transactional;

@Repository
public class MovieRepository {
	
	private static final Logger LOGGER = LoggerFactory.getLogger(MovieRepository.class);
	
	@PersistenceContext
	EntityManager entityManager;

	@Transactional
	public void persist(Movie movie) {
		LOGGER.trace(String.format("em.contains() : %b", entityManager.contains(movie)));
		entityManager.persist(movie);
		LOGGER.trace(String.format("em.contains() : %b", entityManager.contains(movie)));
	}
	
	// ...
	
}
```

Il est alors nécessaire d'ajouter la ligne suivante à la configuration des logs :

```
<logger name="io.github.chrisscientist.hibernate.tutorial.repository.MovieRepository" level="TRACE" />
```
