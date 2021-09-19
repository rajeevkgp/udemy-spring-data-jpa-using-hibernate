# udemy-spring-data-jpa-using-hibernate

ORM - Process of mapping a class to database table, object to table rows and its fields to its columns, once its done we can sync our class objects into database rows, hence we will deal with objects instead of writing sql queries, automatically sql statements will be generated and using jdbc internally, these orm tools will do the insertion, updation, deletion

JPA - Java Persistance API, standard to perform ORM in java applications. It has specifications (for vendors/providers) and API (for developers). There are several JPA providers like hibernate(1), OpenJPA(2), Eclipse Link(3) which implement the JPA api following the specification. Previously we had to learn all (1), (2), (3) depending on which one we want to use, now we learn one JPA api and all the vendors implement the JPA API and we can seamlessly switch from one vendor to another without making any changes to our application. Hibernate is the most popular JPA provider.
Couple of important classes in the JPA API are EntityManagerFactory and EntityManager, annotations like @Entity, @Table for table mapping, @Id, @Column to map fields to table columns.

Developers have the habit of making thing easier for us and removing a lot of boilerplate code. Spring Data is one such framework which removes a lot of configuration and coding hassels when we deal with Data access layer for our applications. Before this we would have to use EntityDao, EntityDaoImpl, EntityManagerFactory, EntityManager, DataSource, DriverManagerDataSource for all the Entities that our application has. Now we have to do just two things. 1) Define the domain object or JPA Entity with all the fields and map it to the database table. 2) define an interface and let it extend CRUDRepository. Spring data also makes several things like JPQL, NativeQuery, finderMethods, without writing any sql code we can load data from the database by following simple method conventions. By default spring data jpa uses hibernate vendor which can be changed if required.

JPA Save call will check for existing id in the database, if its there it will not save but update the entity(feature provided by spring data jpa).

Hibernate uses caching to optimize query response time. It uses Level1 Cache at session level and level2 cache at session factory level. L1 cache is enabled by default. L2 cache is common across all the sessions. L1 cache is specific for any session. For enabling L2 cache we need to add caching providers e.g. ehcache.
@Transactional is required for L1 cache to work, because internally it uses hibernate session and l1 cache is stored at session level. To check you can simply query two times and will see the enabled logs once. https://stackoverflow.com/questions/27879451/does-spring-transactional-use-any-hibernate-cache

Id Generators, Generation Strategies
AUTO - consult the underlying database for generation strategy, whatever the db is using 
IDENTITY - Use auto increment ID column of table to generate, to use this you must set id as primary key auto_increment otherwise the error would be : The database returned no natively generated identity value
SEQUENCE - get the latest id, increment and save
TABLE - create a separate table in mysql for id generation, provide the details in the entity class
We can create a custom id generation by creating a class and extending IdentifierGenerator

Transaction Should be ACID