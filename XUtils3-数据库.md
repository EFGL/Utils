本文为作者原创,转载请指明出处: 
http://blog.csdn.net/a1002450926/article/details/50341173

上一篇文章，主要介绍了XUtil3的注解模块，网络模块，图片加载模块，今天给大家带来数据库模块的讲解，
现在主流的ORM框架很多，比如OrmLite,GreenDao,Active Android,Realm等等，
这些框架每个都有自己的优点和缺点，大家完全可以根据自己项目的实际需求进行选择，下面开始进入今天的数据库模块的介绍。

今天主要给大家带来以下几个模块: 
如何创建删除一张表 
如何对表进行增删查改操作 
如何创建数据库和删除数据库 
如何建立一表对一表，多表对一表，多表对多表的外键操作。 
相信对ORM框架有过了解的人，大概都知道只要创建一个JavaBean对象，在类的上面和属性的上面添加注释标签，这样就能生成一个表。
下面带大家看一下XUtils3的实体bean的写法:
```
@Table(name="person")
public class PersonTable {
    @Column(name="id",isId=true,autoGen=true)
    private int id;
    //姓名
    @Column(name="name")
    private String name;

    //年龄
    @Column(name="age")
    private int age;

    //性别
    @Column(name="sex")
    private String sex;

    //工资
    @Column(name="salary")
    private String salary;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }


    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }


    public String getSalary() {
        return salary;
    }

    public void setSalary(String salary) {
        this.salary = salary;
    }

    @Override
    public String toString() {
        return "PersonTable [id=" + id + ", name=" + name + ", age=" + age
                + ", sex=" + sex + ", salary=" + salary + "]";
    }
}
```
通过上方的实体bean,我们需要知道一个表对应的实体bean需要注意以下几点: 
1.在类名上面加入@Table标签，标签里面的属性name的值就是以后生成的数据库的表的名字 
2.实体bean里面的属性需要加上@Column标签，这样这个标签的name属性的值会对应数据库里面的表的字段。 
3.实体bean里面的普通属性，如果没有加上@Column标签就不会在生成表的时候在表里面加入字段。 
4.实体bean中必须有一个主键，如果没有主键，表以后不会创建成功，@Column(name=”id”,isId=true,autoGen=true)这个属性name的值代表的是表的主键的标识，isId这个属性代表的是该属性是不是表的主键，autoGen代表的是主键是否是自增长，如果不写autoGen这个属性，默认是自增长的属性。

既然知道怎么写实体bean了，下面看看如何在程序中创建一个数据库和如何生成表的吧。

```
public class XUtil {
    static DbManager.DaoConfig daoConfig;
    public static DaoConfig getDaoConfig(){
        File file=new File(Environment.getExternalStorageDirectory().getPath());
        if(daoConfig==null){
            daoConfig=new DbManager.DaoConfig()
            .setDbName("shiyan.db")
            .setDbDir(file)
            .setDbVersion(1)
            .setAllowTransaction(true)
            .setDbUpgradeListener(new DbUpgradeListener() {
                @Override
                public void onUpgrade(DbManager db, int oldVersion, int newVersion) {

                }
            });
        }
        return daoConfig;
    }
}
```
通过XUti.getDaoConfig()方法，我们能够获取到一个DaoConfig对象。通过getDaoConfig()方法，我们可以知道这个方法主要可以做以下事情: 
1.setDbName 设置数据库的名称 
2.setDbDir 设置数据库存放的路径 
3.setDbVersion 设置数据库的版本 
4.setAllowTransaction(true) 设置允许开启事务 
5.setDbUpgradeListener 设置一个版本升级的监听方法 
那么具体我们什么时候创建的表呢？如果我们单纯的调用XUti.getDaoConfig()方法是不能够创建PersonTable这个实体对应的person这张表的，那么如何创建表呢？ 
只需要一下几步: 
1.DaoConfig daoConfig=XUtil.getDaoConfig(); 
2.DbManager db = x.getDb(daoConfig); 
这里我要告诉大家的是，数据库里面表的创建的时间，只有在你对数据库里面的操作涉及到这张表的操作时，会先判断当前的表是否存在，如果不存在，才会创建一张表，如果存在，才会进行相应的CRUD操作，但是只要我们想进行一张表的CRUD操作，我们必须先执行上面的2步，通俗点说就是必须拿到一个Dbmanger这个对象，我为什么这么说呢？那么咱们就先看一下DbManger的庐山真面目吧。 
DbManager部分源码如下:
```
public interface DbManager extends Closeable {

    DaoConfig getDaoConfig();

    SQLiteDatabase getDatabase();

    /**
     * 保存实体类或实体类的List到数据库,
     * 如果该类型的id是自动生成的, 则保存完后会给id赋值.
     *
     * @param entity
     * @return
     * @throws DbException
     */
    boolean saveBindingId(Object entity) throws DbException;

    /**
     * 保存或更新实体类或实体类的List到数据库, 根据id对应的数据是否存在.
     *
     * @param entity
     * @throws DbException
     */
    void saveOrUpdate(Object entity) throws DbException;

    /**
     * 保存实体类或实体类的List到数据库
     *
     * @param entity
     * @throws DbException
     */
    void save(Object entity) throws DbException;

    /**
     * 保存或更新实体类或实体类的List到数据库, 根据id和其他唯一索引判断数据是否存在.
     *
     * @param entity
     * @throws DbException
     */
    void replace(Object entity) throws DbException;

    ///////////// delete
    void deleteById(Class<?> entityType, Object idValue) throws DbException;

    void delete(Object entity) throws DbException;

    void delete(Class<?> entityType) throws DbException;

    void delete(Class<?> entityType, WhereBuilder whereBuilder) throws DbException;

    ///////////// update
    void update(Object entity, String... updateColumnNames) throws DbException;

    void update(Object entity, WhereBuilder whereBuilder, String... updateColumnNames) throws DbException;

    ///////////// find
    <T> T findById(Class<T> entityType, Object idValue) throws DbException;

    <T> T findFirst(Class<T> entityType) throws DbException;

    <T> List<T> findAll(Class<T> entityType) throws DbException;

    <T> Selector<T> selector(Class<T> entityType) throws DbException;

    DbModel findDbModelFirst(SqlInfo sqlInfo) throws DbException;

    List<DbModel> findDbModelAll(SqlInfo sqlInfo) throws DbException;

    ///////////// table

    /**
     * 删除表
     *
     * @param entityType
     * @throws DbException
     */
    void dropTable(Class<?> entityType) throws DbException;

    /**
     * 添加一列,
     * 新的entityType中必须定义了这个列的属性.
     *
     * @param entityType
     * @param column
     * @throws DbException
     */
    void addColumn(Class<?> entityType, String column) throws DbException;

    ///////////// db

    /**
     * 删除库
     *
     * @throws DbException
     */
    void dropDb() throws DbException;

    /**
     * 关闭数据库,
     * xUtils对同一个库的链接是单实例的, 一般不需要关闭它.
     *
     * @throws IOException
     */
    void close() throws IOException;

    ///////////// custom
    void execNonQuery(SqlInfo sqlInfo) throws DbException;

    void execNonQuery(String sql) throws DbException;

    Cursor execQuery(SqlInfo sqlInfo) throws DbException;

    Cursor execQuery(String sql) throws DbException;
}
```
通过DbManager这个类我们知道主要它做了以下几件事情: 
1.getDaoConfig 获取数据库的配置信息 
2.getDatabase 获取数据库实例 
3.saveBindingId saveOrUpdate save 插入数据的3个方法(保存数据) 
4.replace 只有存在唯一索引时才有用 慎重 
5.delete操作的4种方法(删除数据) 
6.update操作的2种方法(修改数据) 
7.find操作6种方法(查询数据) 
8.dropTable 删除表 
9.addColumn 添加一列 
10.dropDb 删除数据库

#插入操作
```
private void insert() {
        try {
            PersonTable person=new PersonTable();
            person.setName("小丽");
            person.setAge(19);
            person.setSex("woman");
            person.setSalary(4000);
            db.save(person);
          //db.saveOrUpdate(person);
          //db.saveBindingId(person);
        } catch (DbException e) {
            e.printStackTrace();
        }
    }
```
![](http://i.imgur.com/BmEiQhr.png)









