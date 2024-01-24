# Python_final_Beste_Yksl
Python dersi kapsamında tarafımca qgis programında python kodları ile oluşturduğum çalışmayı içermektedir.

Ankara iline ait mahalle haritasında Plevne Mahallesine ait veriler doğrultusunda hazırlanan çalışma ve ona ilişkin görseller yer almaktadır.

Yani, bu uygulama belirli bir poligonu seçer, etrafına bir buffer oluşturur ve istenirse sonucu QGIS projeye yükler. Bu, QGIS'deki Python ile jeo-işleme araçlarını otomatikleştirmenin temel bir örneğidir.
Daha sonra izlediğinm adımları GitHub hesabında oluşturduğum Python-Final-Beste adlı repository’de oluşturduğum Readme.md dosyasında açtım.
# Python Final Projesi - Beste
Bu repository, Python Final Projesi kapsamında gerçekleştirilen coğrafi bilgi sistemleri (GIS) uygulamasını içermektedir. Proje, QGIS kullanılarak belirli bir vektör katmanındaki özel bir alanın etrafında tampon oluşturma işlemini gerçekleştirmektedir.


Kullanılan kodlar ;

import processing
# Set the input and output file paths
input_layer_path ='C:/Users/beste/OneDrive/Desktop/workshop-20231220T101756Z 001/workshop/ankara_mahalleler.shp'
output_layer_path='C:/Users/beste/OneDrive/Desktop/workshop-20231220T101756Z 001/workshop/Plevne_output.shp'
# Set the buffer distance in meters
buffer_distance = 100  # Adjust this value as needed
# Set the attribute value to identify the specific polygon
attribute_field = 'NAME'  # Change 'name' to the actual field name you want to use
attribute_value = 'Plevne Mh.'  # Change 'specific_polygon' to the desired attribute value
# Load the input layer
input_layer = QgsVectorLayer('C:/Users/beste/OneDrive/Desktop/workshop-20231220T101756Z-001/workshop/ankara_mahalleler.shp','input_polygon','ogr')
# Select the specific polygon based on the attribute value
expression = f'"{attribute_field}" = \'{attribute_value}\''
input_layer.selectByExpression(expression)
# Create a new layer with only the selected features
selected_layer = processing.run("native:saveselectedfeatures", {
    'INPUT': input_layer,
    'OUTPUT': 'memory:'})['OUTPUT']
# Run the buffer algorithm on the selected layer
processing.run("native:buffer", {
