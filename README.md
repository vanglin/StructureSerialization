# Structure serialization

## Description

This repo is used to serialize the structure in C and becomes easy to access its members by name.
For example:
```
typedef struct _SStudent {
    int id;
    bool sex;
    char name[64];
} SStudent;

You can use a string like 'SStudent.id' to access the member id with an object address.
'SStudent.id' defines the offset position in this structure.
```

## Purpose

1. To solve the access to structure members(like tree) in shared memory, the store data is like below:
```
--------------------------------------------------------------------
| structure offsets for all of members | start address of the data |
--------------------------------------------------------------------
```

2. Can easy access the structure members in config file
```
<xml>
<table>
<row>[% SStudent.id %]<row>
<row>[% SStudent.sex %]<row>
<row>[% SStudent.name %]<row>
</table>
</xml>
```

## Design

1. define all of data in a xml file(name, type, size, etc)
2. load the xml file
3. auto convert the entire xml object into one structure in ssstruct.h
4. auto generate the maps between name with offset in ssmeta.h
5. define API to access the data by serialized name, e.g. School.Grade[i].Class[j].Student[k].id to find the id of the student id at Class.j,Grade.i
