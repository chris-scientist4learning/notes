---
layout: default
title: "Liens utiles - Convertisseur"
permalink: /formation/hibernate/converter/
lang: fr
my_menu: menu-hibernate.html
---

## Convertisseur

### Convertisseur pour les énumérations : exemple

#### Extrait de code de l'entité

```
package io.github.chrisscientist.hibernate.tutorial.domain;

@Entity
public class Movie {

    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE)
    private Long id;

    /* ... */

    @Enumerated(EnumType.STRING)
    private Classification classification;

    /* ... */

}
```

#### Extrait de code la classe de configuration

```
@Bean
public LocalContainerEntityManagerFactoryBean entityManagerFactory() {
    LocalContainerEntityManagerFactoryBean em = new LocalContainerEntityManagerFactoryBean();
    em.setDataSource(dataSource());
    em.setPackagesToScan(new String[] {
        "io.github.chrisscientist.hibernate.tutorial.domain",
        "io.github.chrisscientist.hibernate.tutorial.converter"
    });
    JpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
    em.setJpaVendorAdapter(vendorAdapter);
    em.setJpaProperties(additionalProperties());

    return em;
}
```

#### Code de l'énumération

```
package io.github.chrisscientist.hibernate.tutorial.domain;

public enum Classification {
    TOUS_PUBLIC(1, "Tous public"),
    PUBLIC_AVERTI(2, "Public averti (interdit aux moins de 10 ans)"),
    ACCORD_PARENTAL(3, "Accord parental"),
    INTERDIT_MOINS_12(4, "Inderdit aux moins de 12 ans"),
    INTERDIT_MOINS_16(5, "Interdit aux moins de 16 ans"),
    INTERDIT_MOINS_18(6, "Interdit aux moins de 18 ans");

    private Integer key;
    private String description;

    private Classification(Integer key, String description) {
        this.key = key;
        this.description = description;
    }

    public Integer getKey() {
        return this.key;
    }

    public String getDescription() {
        return this.description;
    }

    public static Classification getClassificationFromKey(Integer aKey) {
        return Arrays.stream(Classification.values())
            .filter(valeur -> valeur.getKey().equals(aKey))
            .findFirst()
            .orElse(null);
    }

}
```

#### Code du convertisseur

```
package io.github.chrisscientist.hibernate.tutorial.converter;

@Converter(autoApply = true)
public class ClassificationAttributeConverter implements AttributeConverter<Classificiation, Integer> {

    @Override
    public Integer convertToDatabaseColumn(Classificiation attribute) {
        return attribute != null ? attribute.getKey() : null;
    }

    @Override
    public Classificiation convertToEntityAttribute(Integer dbData)
    {
        return Classification.getClassificationFromKey(dbData);
    }

}
```



