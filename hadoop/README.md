# **PASOS PARA REALIZAR UN CONTEO DE PALABRAS EN UN LIBRO CON APACHE HADOOP**
![Hadoop_logo svg](https://github.com/user-attachments/assets/7f35eb58-c333-4a81-9b46-6843c3a1e9a6)

### **Estos pasos se realizaron para el ejercicio en la sesion entonces ya no son necesarios de ejecutar pero se añaden como referencia:**

##### 1. Obtener la imagen de Docker con hadoop usando el comando pull docker image

```
sudo docker pull uracilo/hadoop
```

##### 2. Clonar repositorio github.

```
git clone https://github.com/uracilo/hadoop.git
```

##### 3. Creamos la red para el cluster que usaremos de hadoop.

```
sudo docker network create --driver=bridge hadoop
```

##### 4.  Entramos al directorio hadoop

```
cd hadoop
```
***
### **A partir de aqui se muestran los pasos que se realizaron para la practica de tarea:**

##### 5. Iniciar el contenedor e iniciar hadoop

```
./start-container.sh
./start-hadoop.sh
```

##### 6. Obtenemos el archivo txt de cada libro
📚**Libro Alicia:**
```
wget https://www.gutenberg.org/cache/epub/28885/pg28885.txt
```
📚**Libro The war drama of the Eagles:**
```
wget https://www.gutenberg.org/cache/epub/75293/pg75293.txt
```
##### 7. Creamos un directorio para nuestro input

```
mkdir input
```

##### 8. Crear un archivo tipo tar.gz para cada libro

📚Libro Alicia:
```
tar -czvf input/odisea.tar.gz pg28885.txt
```
📚Libro The war drama of the Eagles:
```
tar -czvf input/war.tar.gz pg75293.txt
```

##### 9. Revisar que esten y revisar los tamaños de nuestros archivos

```
ls -flarts input
```
##### 10. Crear y mover directorio input al DFS de HADOOP

```
hdfs dfs -mkdir -p test
hdfs dfs -put input
```

##### 11. Revisamos los archivos en nuestro directorio input

```
hdfs dfs –ls  input
```

##### 12. Leemos las ultimas 20 lineas de nuestros libros
📚Libro de Alicia:
```
hdfs dfs -cat  input/alicia.tar.gz | zcat | tail -n 20
```
📚Libro The war drama of the Eagles:
```
hdfs dfs -cat  input/war.tar.gz | zcat | tail -n 20
```

##### 13. Ejecutamos el trabajo de conteo de palabras de hadoop

```
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/sources/hadoop-mapreduce-examples-2.7.2-sources.jar org.apache.hadoop.examples.WordCount input output
```

##### 14. Ejecutamos el comando para ver el resultado del trabajo

```
hdfs dfs -cat output/part-r-00000
```

#### Resultados obtenidos de cada libro:

📚Libro de Alicia:
![imagen](https://github.com/user-attachments/assets/f7b7bcb0-1c06-426e-9467-99e3e8e919cd)

📚Libro The war drama of the Eagles:
![imagen](https://github.com/user-attachments/assets/1be99ec6-011d-4fb4-93f0-8bb733084cf8)

