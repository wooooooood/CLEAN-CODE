# Using
> https://stackoverflow.com/questions/22325290/multiple-using-block-c-sharp

### BEFORE
```
using (SqlConnection con = new SqlConnection(connectionString))
{
    using(SqlCommand com = new SqlCommand("",con))
    {
        using (SqlDataReader sdr = com.ExecuteReader())
        {
        }
    }
}
```

### AFTER
```
using (SqlConnection con = new SqlConnection(connectionString))
using(SqlCommand com = new SqlCommand("",con))
using (SqlDataReader sdr = com.ExecuteReader())
{
}
```  
  
- IDisposable한 요소들 중, using을 사용하면 Exception 여부와 상관없이 dispose됨
- Try-catch가 필요없음, 뭔가 catch해서 처리하고 싶을때만 사용
  > *Pokemon exception handling... "Gotta catch em all"* https://stackoverflow.com/a/22325345
