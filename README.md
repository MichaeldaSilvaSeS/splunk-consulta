# splunk-consulta


(?:\"|\')(?<key>[^"]*)(?:\"|\')(?=:)(?:\:\s*)(?:\"|\')?(?<value>true|false|[0-9a-zA-Z\+\-\,\.\$]*)


index="ip_search" | rename _time as DataHoraLog | spath input=Log output=Tipo path=tipo | fillnull value="Indefinido" Tipo | iplocation IP | rename City As Cidade | rename Region as Estado | rename lat as Latitude | rename lon as Longitude | sort DataHoraLog, CorrelationId | table CorrelationId , IP, Latitude, Longitude, Cidade, Estado | geostats count latfield=Latitude longfield=Longitude

index="ip_search" | rename _time as DataHoraLog | spath input=Log output=Tipo path=tipo | fillnull value="Indefinido" Tipo | iplocation IP | rename City As Cidade | rename Region as Estado | rename Country as Pais | rename lat as Latitude | rename lon as Longitude | sort DataHoraLog, CorrelationId | table CorrelationId , IP, Latitude, Longitude, Cidade, Estado, Pais | stats count by Pais | geom geo_countries featureIdField=Pais

index="ip_search" | rename _time as DataHoraLog | spath input=Log output=Tipo path=tipo | fillnull value="Indefinido" Tipo | iplocation IP | rename City As Cidade | rename Region as Estado | rename Country as Pais | rename lat as Latitude | rename lon as Longitude | sort DataHoraLog, CorrelationId | table CorrelationId , IP, Latitude, Longitude, Cidade, Estado, Pais | stats count by Pais | geom geo_countries featureIdField=Pais | search Pais="Brazil"

index="ip_search" | iplocation IP | rename City As featureId | stats count by featureId | geom lookup_municipios_sem_acento allFeatures=true
