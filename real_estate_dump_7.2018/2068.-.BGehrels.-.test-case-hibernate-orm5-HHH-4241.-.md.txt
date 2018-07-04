# Hibernate Test Case For HHH-4241

If a sub class of a ``@Inheritance(strategy = SINGLE_TABLE)`` contains fields from multiple secondary tables, the join 
order depends on the hashCode of their table names. Hibernate ignores the ``optional=false`` annotations, which leads to
missing entries in the result set.

Given that ``MANDATORY_TABLE`` is a secondary table that *must* always be present and ``energy_certificates`` is a 
secondary table that may have entries or not. In the test case provided here hibernate generates the following 
statement:
 
     select
         baseclass_1_.OPTIONAL_TABLE_FIELD as OPTIONAL1_1_,
         baseclass_2_.mandatoryTableField as mandator1_2_ 
     from
         energy_certificates baseclass_1_ 
     inner join
         mandatory_table baseclass_2_ 
             on baseclass_1_.REAL_ESTATE_ID=baseclass_2_.ID 
     where
         baseclass_1_.REAL_ESTATE_ID=?
         
Given the above semantics of the tables, the following statement would have been appropriate:
 
     select
         baseclass_1_.OPTIONAL_TABLE_FIELD as OPTIONAL1_1_,
         baseclass_2_.mandatoryTableField as mandator1_2_ 
     from
         mandatory_table baseclass_1_ 
     left outer join
         energy_certificates baseclass_2_ 
             on baseclass_2_.REAL_ESTATE_ID=baseclass_1_.ID 
     where
         baseclass_1_.REAL_ESTATE_ID=?
