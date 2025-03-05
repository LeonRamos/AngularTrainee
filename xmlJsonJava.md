Los formatos XML y JSON son ampliamente utilizados para el intercambio de datos entre aplicaciones. Ambos tienen sus propias características, ventajas y desventajas. Veamos un ejemplo de cada uno y sus principales diferencias:

## Ejemplo en XML

```xml


  
    Cien años de soledad
    Gabriel García Márquez
    1967
  
  
    El principito
    Antoine de Saint-Exupéry
    1943
  

```

## Ejemplo en JSON

```json
{
  "biblioteca": {
    "libros": [
      {
        "titulo": "Cien años de soledad",
        "autor": "Gabriel García Márquez",
        "anio": 1967
      },
      {
        "titulo": "El principito",
        "autor": "Antoine de Saint-Exupéry",
        "anio": 1943
      }
    ]
  }
}
```

## Principales diferencias

1. **Estructura**: XML utiliza etiquetas para definir elementos y atributos, mientras que JSON usa pares clave-valor y arrays.

2. **Legibilidad**: JSON tiende a ser más conciso y fácil de leer para humanos, mientras que XML puede ser más verboso[5][8].

3. **Procesamiento**: JSON es generalmente más rápido de procesar y requiere menos recursos, lo que lo hace más eficiente para aplicaciones web y móviles.

4. **Tipos de datos**: JSON admite tipos de datos como números, booleanos, arrays y objetos de forma nativa, mientras que XML trata todo como texto.

5. **Compatibilidad**: JSON es más compatible con JavaScript y es ampliamente utilizado en desarrollo web moderno, mientras que XML tiene mayor soporte en aplicaciones empresariales tradicionales.

6. **Validación**: XML tiene un sistema de validación más robusto a través de esquemas XSD, mientras que JSON tiene opciones de validación más limitadas.

Para codificar un ejemplo en Google Colab, puedes usar el siguiente código Python que demuestra cómo trabajar con ambos formatos:

```python
import json
import xml.etree.ElementTree as ET

# Crear datos en formato JSON
json_data = {
  "biblioteca": {
    "libros": [
      {
        "titulo": "Cien años de soledad",
        "autor": "Gabriel García Márquez",
        "anio": 1967
      },
      {
        "titulo": "El principito",
        "autor": "Antoine de Saint-Exupéry",
        "anio": 1943
      }
    ]
  }
}

# Convertir JSON a string y luego a XML
json_string = json.dumps(json_data)
root = ET.Element("root")
ET.SubElement(root, "json").text = json_string
xml_string = ET.tostring(root, encoding="unicode")

print("JSON:")
print(json.dumps(json_data, indent=2))
print("\nXML:")
print(xml_string)
```

Aquí tienes un ejemplo de uso con JavaScript para el intercambio de información entre XML y JSON:

```javascript
// Ejemplo de datos en formato XML
const xmlString = `

  
    Cien años de soledad
    Gabriel García Márquez
    1967
  
  
    El principito
    Antoine de Saint-Exupéry
    1943
  
`;

// Función para convertir XML a JSON
function xmlToJson(xml) {
  const parser = new DOMParser();
  const xmlDoc = parser.parseFromString(xml, "text/xml");
  
  function convertToJson(node) {
    const obj = {};
    if (node.nodeType === 1) { // element node
      if (node.attributes.length > 0) {
        obj["@attributes"] = {};
        for (let j = 0; j ";
    if (json[prop] instanceof Array) {
      for (let array of json[prop]) {
        xml += "";
        xml += jsonToXml(new Object(array));
        xml += "";
      }
    } else if (typeof json[prop] === "object") {
      xml += jsonToXml(new Object(json[prop]));
    } else {
      xml += json[prop];
    }
    xml += json[prop] instanceof Array ? '' : "";
  }
  return xml;
}

// Convertir JSON de vuelta a XML
const xmlData = jsonToXml(jsonData);
console.log("JSON a XML:", xmlData);
```

Este ejemplo demuestra cómo convertir datos entre formatos XML y JSON utilizando JavaScript. El código incluye dos funciones principales:

1. `xmlToJson`: Esta función toma una cadena XML y la convierte en un objeto JSON. Utiliza el `DOMParser` para analizar el XML y luego recorre recursivamente la estructura del documento para construir el objeto JSON correspondiente.

2. `jsonToXml`: Esta función realiza la operación inversa, convirtiendo un objeto JSON de vuelta a una cadena XML. Recorre recursivamente el objeto JSON y construye las etiquetas XML apropiadas.

El ejemplo comienza con una cadena XML que representa una biblioteca con dos libros. Luego, convierte este XML a JSON, lo imprime en la consola, y finalmente convierte el JSON de vuelta a XML.

