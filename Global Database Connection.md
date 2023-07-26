# Database Connection In Asp.net MVC

#### 1. In Web Config File ####

 ```
<connectionStrings>

  <add name="MySqlConnection"
       connectionString="Server=MYSQL5047.site4now.net;Database=db_a9b37b_demo;Uid=a9b37b_demo;Pwd=pass@123;"
       providerName="MySql.Data.MySqlClient"/>

 </connectionStrings>

 ```
#### 2. In Context Classess or Data Access Layer Classes ####
```
string ConnectionString = ConfigurationManager.ConnectionStrings["MySqlConnection"].ConnectionString;
```

#### 3. Controllers Classess ####
```
connectionHelper connectionHelper = new connectionHelper();
or
DataAccessLayer dbcontext = new DataAccessLayer();

```

#### 4. Examples for Use in Controller ####
```
 public ActionResult SaveData()
 {
  connectionHelper.SaveDataEntries(dataEntries);
  return View("Index");
 }

```

#### 4. Examples for Use in DataAccess Layer class ####
```
  public void SaveDataEntries(List<DataEntry> dataEntries)
        {
            using (var connection = new MySqlConnection(ConnectionString))
            {
                connection.Open();

                foreach (var dataEntry in dataEntries)
                {
                    using (var command =
                    new MySqlCommand("INSERT INTO DataEntries (Name, Description) VALUES (@Name, @Description)", connection))
                    {
                        command.Parameters.AddWithValue("@Name", dataEntry.Name);
                        command.Parameters.AddWithValue("@Description", dataEntry.Description);

                        command.ExecuteNonQuery();
                    }
                }
            }
        }

```



