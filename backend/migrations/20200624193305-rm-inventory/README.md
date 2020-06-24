# Migration `20200624193305-rm-inventory`

This migration has been generated by Angad Singh at 6/24/2020, 7:33:05 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE `cryptocracy`.`Inventory` DROP FOREIGN KEY `Inventory_ibfk_1`;

DROP TABLE `cryptocracy`.`Inventory`;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200621172701-init..20200624193305-rm-inventory
--- datamodel.dml
+++ datamodel.dml
@@ -1,7 +1,7 @@
 datasource db {
   provider = "mysql"
-  url = "***"
+  url      = env("MYSQL_URL")
 }
 generator client {
   provider = "prisma-client-js"
@@ -56,9 +56,8 @@
   hasHintCard     Boolean   @default(false)
   currentTileId   Int
   currentTile     Tile      @relation(fields: [currentTileId], references: [id])
-  inventory     Inventory[]
   logs          Log[]
   levels        UserLevel[]
   riddles       UserRiddle[]
   visitedTiles  VisitedTile[]
@@ -182,19 +181,8 @@
   key       String   @unique
   value     Json
 }
-model Inventory {
-  id        Int      @id @default(autoincrement())
-  createdAt DateTime @default(now())
-  updatedAt DateTime @updatedAt @default(now())
-  hex       String
-  userId    Int
-  user      User     @relation(fields: [userId], references: [id])
-  item      String
-  used      Boolean  @default(false)
-}
-
 model Log {
   id        Int      @id @default(autoincrement())
   createdAt DateTime @default(now())
   updatedAt DateTime @updatedAt @default(now())
```

