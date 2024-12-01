# Nodo 1
mongod --replSet rs0 --dbpath="C:\data\db\db1" --port 27017

# Nodo 2
mongod --replSet rs0 --dbpath="C:\data\db\db2" --port 27018

# Nodo 3
mongod --replSet rs0 --dbpath="C:\data\db\db3" --port 27019

// Conectar al nodo primario
mongosh --host localhost --port 27017

// Inicializar el Replica Set
rs.initiate()

// Agregar segundo nodo
rs.add("localhost:27018")

// Agregar tercer nodo
rs.add("localhost:27019")

// Comprobar estado
rs.status()

// Conectar al nodo primario
use torneoBaloncesto
db.arbitros.insert({
    nombre: "Miguel Suárez",
    nacionalidad: "Colombiana",
    experiencia: 5
})

// Conectar al nodo secundario (localhost:27019)
use torneoBaloncesto
db.arbitros.find()

db.arbitros.deleteOne({ nombre: "Miguel Suárez" })

// Verificar en nodo primario o cualquier otro nodo secundario
db.arbitros.find()
