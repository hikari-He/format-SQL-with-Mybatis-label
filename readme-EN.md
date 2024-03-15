[中文 readme](README.md)
# a simple javascript to format SQL with mybatis's XML label

This program is used to format (or expand) the collapsed mybatis SQL statements to facilitate human reading or modification. Note that the mybatis SQL mentioned here refers to SQL statements with mybatis XML tags, such as `<select>`, `<foreach>`, etc.

His input is a line of mybatis SQL statement, and the output is the formatted mybatis SQL statement.

Input example:
```
<select id="getSomeThing" resultType="map"> select distinct a.name_order as "nameorder", #{authId}  as "authid", trim(authType) as "authType", concat('org-', a.org_icon) as "org" from table_user a left join (select b.obj_type, b.obj_id from table_object a left join table_auth_data b on a.auth_id = b.id where a.auth = concat('a', concat('b', 'c'))) b on (b.obj_type = trim(a.auth_type) and b.object_id = aa)  where a.parent is null and(1=1 and <if test="idCode != null and idCode != ''"> AND f.idCode LIKE concat('%', concat(#{idCode},'%')) </if> <if test="testName != null and testCode != ''"> AND f.testName LIKE concat('%', concat(#{testName},'%')) </if> ) and trim(c.org_id) = #{org_Id} order by a.order asc </select>
```

Output example:

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

NOTE: This program cannot format statements annotated with '--some annotation'.

In order to facilitate everyone to test or add this code to their own complex projects, I publish it as an HTML file. You can open it directly using your browser and test it.