Comprueba con dig o nslookup que:

• Puedes resolver los registros tipo A.
![alt text](image.png)

• Comprueba que se pueden resolver de forma inversa sus direcciones IP.
![alt text](image-1.png)

• Puedes resolver los alias ns1.sistema.test y ns2.sistema.test.
![alt text](image-2.png)
![alt text](image-3.png)

• Realiza la consulta para saber los servidores NS de sistema.test. Debes obtener
tierra.sistema.test y venus.sistema.test.
![alt text](image-4.png)

• Realiza la consulta para saber los servidores MX de sistema.test.
![alt text](image-5.png)

• Comprueba que se ha realizado la transferencia de la zona entre el servidor DNS maestro y el
esclavo. Revisa los logs o realiza una consulta del registro AXFR.

• Comprueba que tanto maestro como esclavo pueden contestar a las mismas preguntas.