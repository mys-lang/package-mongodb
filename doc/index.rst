|discord|_
|test|_
|stars|_

About
=====

MongoDB client in the `Mys programming language`_.

Project: https://github.com/mys-lang/package-mongodb

Examples
========

List databases
--------------

.. code-block:: mys

   from mongodb import Client

   func main():
       client = Client()
       client.connect()
       print(client.list_databases())
       client.disconnect()

List collections
----------------

.. code-block:: mys

   from mongodb import Client

   func main():
       client = Client()
       client.connect()
       print(client.list_collections("database"))
       client.disconnect()

Drop collection
---------------

.. code-block:: mys

   from mongodb import Client

   func main():
       client = Client()
       client.connect()
       client.drop("database", "collection")
       client.disconnect()

Insert documents
----------------

.. code-block:: mys

   from bson import Array
   from bson import Boolean
   from bson import Document
   from mongodb import Client

   func main():
       client = Client()
       client.connect()
       client.insert("database",
                     "collection",
                     Array([
                         Document([("x", Boolean(True))]),
                         Document([("x", Boolean(False))])
                     ]))
       client.disconnect()

Find documents
--------------

.. code-block:: mys

   from bson import Boolean
   from bson import Document
   from mongodb import Client

   func main():
       client = Client()
       client.connect()
       filter = Document([("x", Document([("$eq", Boolean(False))]))])
       projection = Document([("_id", Int32(0))])
       documents = client.find_many("database",
                                    "collection",
                                    filter=filter,
                                    projection=projection)

       for document in documents:
           print(document.get("x").get_boolean())

       client.disconnect()

Delete documents
----------------

.. code-block:: mys

   from bson import Array
   from bson import Boolean
   from bson import Document
   from bson import Int32
   from mongodb import Client

   func main():
       client = Client()
       client.connect()
       client.delete("database",
                     "collection",
                     Array([
                         Document([
                             ("q", Document([("x", Boolean(True))])),
                             ("limit", Int32(0))
                         ])
                     ]))
       client.disconnect()

API
===

.. mysfile:: src/lib.mys

.. |discord| image:: https://img.shields.io/discord/777073391320170507?label=Discord&logo=discord&logoColor=white
.. _discord: https://discord.gg/GFDN7JvWKS

.. |test| image:: https://github.com/mys-lang/package-mongodb/actions/workflows/pythonpackage.yml/badge.svg
.. _test: https://github.com/mys-lang/package-mongodb/actions/workflows/pythonpackage.yml

.. |stars| image:: https://img.shields.io/github/stars/mys-lang/package-mongodb?style=social
.. _stars: https://github.com/mys-lang/package-mongodb

.. _Mys programming language: https://mys-lang.org
