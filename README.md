[English readme here](README-EN.md)

# 一个简单的用来格式化带有mybatis XML 标签的SQL语句的JavaScript小程序

这个程序是用来将被折叠的mybatis SQL语句格式化（或者说展开）以方便人类阅读或修改。注意这里所说的mybatis SQL指的是带有mybatis XML 标签的SQL语句，比如`<select>`、`<foreach>`等。

他的输入是一行mybatis SQL语句，输出是格式化后的mybatis SQL语句。

输入示例：

```
<select id="getSomeThing" resultType="map"> select distinct a.name_order as "nameorder", #{authId}  as "authid", trim(authType) as "authType", concat('org-', a.org_icon) as "org" from table_user a left join (select b.obj_type, b.obj_id from table_object a left join table_auth_data b on a.auth_id = b.id where a.auth = concat('a', concat('b', 'c'))) b on (b.obj_type = trim(a.auth_type) and b.object_id = aa)  where a.parent is null and(1=1 and <if test="idCode != null and idCode != ''"> AND f.idCode LIKE concat('%', concat(#{idCode},'%')) </if> <if test="testName != null and testCode != ''"> AND f.testName LIKE concat('%', concat(#{testName},'%')) </if> ) and trim(c.org_id) = #{org_Id} order by a.order asc </select>
```

输出示例：
```
<select id="getSomeThing" resultType="map">
    select distinct
      a.name_order as "nameorder",
      #{authId} as "authid",
      trim(authType) as "authType",
      concat ('org-', a.org_icon) as "org"
    from
      table_user a
      left join (
        select
          b.obj_type,
          b.obj_id
        from
          table_object a
          left join table_auth_data b on a.auth_id = b.id
        where
          a.auth = concat ('a', concat ('b', 'c'))
      ) b on (
        b.obj_type = trim(a.auth_type)
        and b.object_id = aa
      )
    where
      a.parent is null
      and(1=1 and
    <if test="idCode != null and idCode != ''">
        AND f.idCode LIKE concat ('%', concat (#{idCode}, '%'))
    </if>
    
    <if test="testName != null and testCode != ''">
        AND f.testName LIKE concat ('%', concat (#{testName}, '%'))
    </if>
)    and trim(c.org_id) = #{org_Id}
    order by
      a.order asc
</select>
```

注意：此程序无法格式化带有'--some annotation'注释的语句。

为了方便大家测试或者将这段代码加入自己的复杂项目，我以HTML文件的方式发布。你可以直接使用浏览器打开它并进行测试。