# Playing-with-Geometry-Spatial_Data_Types_in_MySQL

## Buat Tabel

CREATE TABLE `epantau` (
  `no` int(11) NOT NULL,
  `keterangan` varchar(50) NOT NULL,
  `latitude` varchar(25) DEFAULT NULL,
  `latitude_end` varchar(25) DEFAULT NULL,
  `longitude` varchar(25) DEFAULT NULL,
  `longitude_end` varchar(25) DEFAULT NULL,
  `geom` point NOT NULL
) ENGINE=MyISAM DEFAULT CHARSET=utf8;

## Buat geometry data dari kolom latitude longitude

ALTER TABLE namatabel add geographyColumn as geography::STGeomFromText('POINT('+convert(varchar(20),Long)+' '+convert(varchar(20),Lat)+')',4326)

## Update column geom berdasarkkan column berisi titik koordinat

UPDATE namatabel SET geom = Point(longitude, latitude);
UPDATE namatabel SET GEOM = geography::Point(longitude, latitude, 4326);

## Modifikasi data column geom

ALTER TABLE namatabel MODIFY geom POINT NOT NULL;

## buat spatial index column geom

CREATE SPATIAL INDEX namadatabase ON namatabel(geom);
