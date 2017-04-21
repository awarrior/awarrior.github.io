Metastore utilizes Datanucleus persistence tool, which supports JDO specification.

several JDO important classes: PersistenceManager/PersistenceManagerFactory

* Level 1 Cache - mandated by the JDO specification, and represents the caching of instances within a PersistenceManager
* Level 2 Cache - represents the caching of instances within a PersistenceManagerFactory (across multiple PersistenceManager's)

org.apache.hadoop.hive.metastore.ObjectStore: pmf = JDOHelper.getPersistenceManagerFactory(prop);

JDOHelper utilizes Java Reflect to get PMF

get PersistenceManagerFactory using properties(according to HiveConf - hive-site.xml), the connection between JDO and Datanucleus is the property called 'javax.jdo.PersistenceManagerFactoryClass'

DataStoreCache dsc = pmf.getDataStoreCache(); # level 2

get level 1 cache(Map< Object, ObjectProvider>) from ExecutionContextImpl
