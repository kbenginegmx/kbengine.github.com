---
layout: docs_cn
title: Defining the Entity · Docs · KBEngine
tab: docs
docsitem: documentation-entitydef
---

Defining the Entity
====================

What needs to be defined Entity:

* Stored in the database

* Ability to facilitate remote access

* Need to manage and monitor its engines, such as: AOI, Trap, etc...

* When a disaster recovery server can automatically recover


You need to perform the following steps:
-----------------------------------------

* Registration

Path definition file : `demo/res/scripts/entities.xml`

Example:

	<root>
		<Account/>
		<Avatar/>
		<Spaces/>
		<Space/>
		<Monster/>
		<NPC/>
		<Gate/>
	</root>


* Def file to create a directory in `res/scripts/entity_defs`

	For example: Account.def

* You may also need to define some properties and methods

	1. In the `demo/res/scripts/`, base and cell or client add xxx.py

	2. Not every entity needs to create three parts(client, base, cell), press need to select.


-----------------------------------------


Def file format
-----------------------------------------

	<root>
		<Properties>
			// Property Name
			<accountName>
				// Property type
				<Type>			UNICODE				</Type>

				// Property Scopes
				<Flags>			BASE				</Flags>

				// Is stored in the database (optional)
				<Persistent>		true				</Persistent>

				// The maximum length is stored in the database (optional)
				<DatabaseLength> 	100				</DatabaseLength>

				// Default value (optional)
				<Default>		kbengine			</Default>

				// mysql Identifier (optional)
				<Identifier>		true				</Identifier>
			</accountName>
			
			...
			...
		</Properties>

		<ClientMethods>
			// remote method Name
			<onReqAvatarList>
				// remote method args type
				<Arg>	AVATAR_INFOS_LIST	</Arg>
			</onReqAvatarList>

			...
			...
		</ClientMethods>

		<BaseMethods>
			// remote method Name
			<reqAvatarList>
				<Exposed/>
			</reqAvatarList>
			
			...
			...
		</BaseMethods>

		<CellMethods>
			<hello>
			</hello>
		</CellMethods>

	</root>

For example: In a client to get a list of server roles(Account.py):

	 self.base.reqAvatarList()


-----------------------------------------


Type Scope
-----------------------------------------

	[name]			[client]		[base]			[cell]
	BASE			-			*			-
	BASE_AND_CLIENT		*			*			-
	CELL_PRIVATE		-			-			*(cell)
	CELL_PUBLIC		-			-			*(cells)
	CELL_PUBLIC_AND_OWN	*(client)		-			*(cells)
	ALL_CLIENTS		*(clients)		-			*(cells)
	OWN_CLIENT		*(client)		-			*(cell)
	OTHER_CLIENTS		*(other clients)	-			*(cells)



-----------------------------------------------

download: 
[rpgdemo_project.tar]



[rpgdemo_project.tar]: {{ site.baseurl }}/assets/other/rpgdemo_project.tar