# laboratorio-sql
-- Listar las pistas (tabla Track) con precio mayor o igual a 1€
	-- SELECT T.Name, T.UnitPrice FROM Track T WHERE T.UnitPrice >= 1;

-- Listar las pistas de más de 4 minutos de duración
	-- SELECT T.Name, T.Milliseconds FROM Track T WHERE T.Milliseconds > 240000;

-- Listar las pistas que tengan entre 2 y 3 minutos de duración
	-- SELECT T.Name, T.Milliseconds FROM Track T WHERE T.Milliseconds BETWEEN 120000 AND 180000;

-- Listar las pistas que uno de sus compositores (columna Composer) sea Mercury
	 -- SELECT T.Name, T.Composer FROM Track T WHERE T.Composer LIKE '%Mercury%';

-- Calcular la media de duración de las pistas (Track) de la plataforma
	 -- SELECT AVG(T.Milliseconds) AS 'Duración Media (ms)' FROM Track T ;

-- Listar los clientes (tabla Customer) de USA, Canada y Brazil
	 -- SELECT C.FirstName, C.Country FROM Customer C WHERE C.Country IN ('USA', 'CANADA', 'BRAZIL');

-- Listar todas las pistas del artista 'Queen' (Artist.Name = 'Queen')
	 -- SELECT Al.Title, Ar.Name FROM Album Al INNER JOIN Artist Ar ON Al.ArtistId = Ar.ArtistId WHERE Ar.Name = 'Queen';

-- Listar las pistas del artista 'Queen' en las que haya participado como compositor David Bowie
	-- SELECT T.Name, T.Composer FROM Track T WHERE T.Composer LIKE '%Queen%David Bowie%';

-- Listar las pistas de la playlist 'Heavy Metal Classic'
	-- SELECT T.Name, P.Name FROM Track T INNER JOIN PlaylistTrack Pt ON T.TrackId = Pt.TrackId 
	-- INNER JOIN Playlist P ON PT.PlaylistId = P.PlaylistId WHERE P.Name = 'Heavy Metal Classic';

-- Listar las playlist junto con el número de pistas que contienen
	-- SELECT P.Name, Count(Pt.TrackId) AS 'Número de pistas' FROM Playlist P INNER JOIN PlaylistTrack Pt ON P.PlaylistId = Pt.PlaylistId GROUP BY P.Name;

-- Listar las playlist (sin repetir ninguna) que tienen alguna canción de AC/DC
	-- SELECT DISTINCT P.Name, T.Name, T.Composer FROM Playlist P INNER JOIN PlaylistTrack Pt ON P.PlaylistId = Pt.PlaylistId
	-- INNER JOIN Track T ON PT.TrackId = T.TrackId WHERE T.Composer LIKE '%AC/DC%'

-- Listar las playlist que tienen alguna canción del artista Queen, junto con la cantidad que tienen
	-- SELECT DISTINCT P.Name, COUNT(Pt.TrackId) AS 'Canciones de Queen' FROM Playlist P INNER JOIN PlaylistTrack Pt ON P.PlaylistId = Pt.PlaylistId
	-- INNER JOIN Track T ON PT.TrackId = T.TrackId WHERE T.Composer LIKE '%Queen%' GROUP BY P.Name; 

-- Listar las pistas que no están en ninguna playlist
	-- SELECT T.Name FROM Track T LEFT JOIN PlaylistTrack pt ON t.TrackID = pt.TrackID WHERE pt.PlaylistID IS NULL;
 ## EXTRAS: 
 -- Listar las pistas ordenadas por el número de veces que aparecen en playlists de forma descendente
	-- SELECT T.Name, COUNT(pt.PlaylistId) AS 'Veces en Playlist' FROM Track T LEFT JOIN PlaylistTrack Pt  ON T.TrackId = Pt.TrackId GROUP BY T.Name ORDER BY COUNT(pt.PlaylistId) DESC;

-- Listar las pistas más compradas (la tabla InvoiceLine tiene los registros de compras)
	-- SELECT T.Name, COUNT(Il.TrackId) AS 'Compras' FROM Track T LEFT JOIN InvoiceLine Il ON T.TrackId = Il.InvoiceLineId GROUP BY T.Name ORDER BY COUNT(Il.TrackId) DESC;

-- Listar los artistas más comprados
	-- SELECT T.Composer, COUNT(Il.TrackId) AS 'Compras' FROM Track T LEFT JOIN InvoiceLine Il ON T.TrackId = Il.InvoiceLineId GROUP BY T.Composer HAVING T.Composer != 'NULL' ORDER BY COUNT(iL.TrackId) DESC;

-- Listar las pistas que aún no han sido compradas por nadie
	-- SELECT T.Name, COUNT(Il.TrackId) AS 'Compras' FROM Track T LEFT JOIN InvoiceLine Il ON T.TrackId = Il.InvoiceLineId GROUP BY T.Name HAVING COUNT(iL.TrackId) = 0;

-- Listar los artistas que aún no han vendido ninguna pista
	-- SELECT T.Composer, COUNT(Il.TrackId) AS 'Compras' FROM Track T LEFT JOIN InvoiceLine Il ON T.TrackId = Il.InvoiceLineId GROUP BY T.Composer HAVING T.Composer != 'NULL' AND COUNT(iL.TrackId) = 0 ORDER BY COUNT(iL.TrackId) DESC;


-- Listar los artistas que no tienen album
	-- SELECT Ar.Name FROM Artist Ar LEFT JOIN Album Al ON Ar.ArtistId = Al.ArtistId WHERE Al.AlbumId IS NULL;

-- Listar los artistas con el número de albums que tienen
	-- SELECT Ar.Name, COUNT(Al.AlbumId) AS 'Número de Álbums' FROM Artist Ar LEFT JOIN Album Al ON Ar.ArtistId = Al.ArtistId GROUP BY Ar.Name;
