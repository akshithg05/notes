# Object Storage

We will delve into what object storage is and where it finds its use in system design interviews. Object storage systems have gained widespread popularity over the past 10-15 years. Object storage is more akin to file storage systems rather than traditional databases.

## Databases VS Object Storage - What's the difference?

In databases, the way we filter and search for data holds significant importance. However, with object storage, the concept of folders doesn't exist. Both databases and object storage can store data, but the key differences lie in the structure, accessibility, and scalability of the data. In a file system, data is organized in a hierarchical structure resembling a tree, where files are stored within folders that can be nested within other folders.

Contrastingly, object storage treats each piece of data as an object, comprising the actual data, metadata, and a unique identifier. There is no hierarchy in object storage, as opposed to a file system. Objects are stored in flat address spaces, which facilitates easier scalability compared to file storage systems, thanks to the absence of hierarchical complexity. Object storage evolved from BLOB (Binary Large Object) storage and is commonly used for storing items such as images, videos, and database backups. Prominent examples include AWS S3 and Google Cloud Storage.

From a design perspective, it's crucial to note that storing images or videos in a database is typically not a recommended practice. Querying for specific images or videos in a database is rare, and storing such data in a database can hinder performance, increase storage requirements, and result in frequent read and write operations on the database.

Traditional RDBMSs are not optimized for handling large files, but object storage emerges as a solution to this challenge. It is specifically designed to handle unstructured data efficiently and is well-suited for storing large files. One significant advantage of using object-based storage is its scalability, allowing for easy scaling of the flat architecture without encountering the limitations associated with file storage.

When retrieving data from an object store, direct reads from the object store itself are typically not performed. Instead, a network HTTP request is made directly to the object storage to fetch the data. In system design interviews, object storage is frequently employed for storing images and videos, such as through Amazon Simple Storage Service (Amazon S3).

# Closing Notes

To recap our discussion on storage, we have explored two widely used types of databases: SQL and NoSQL. We acknowledged that neither is superior to the other, as they have distinct use cases based on specific requirements. Additionally, we delved into important database scaling techniques such as replication and sharding. These techniques enable databases to overcome certain limitations, but they come with their own set of tradeoffs.