# The rarest book is missing!
Assignment 1 Image
This was supposed to be a great day for Digitown’s National Library Museum and all of Digitown.
The museum has just finished scanning more than 325,000 rare books, so that history lovers around the world can experience the ancient culture and knowledge of the Digitown Explorers.
The great book exhibition was about to re-open, when the museum director noticed that he can't locate the rarest book in the world:
"De Revolutionibus Magnis Data", published 1613, by Gustav Kustov.
The mayor of the Digitown herself, Mrs. Gaia Budskott - has called on our agency to help find the missing artifact.

Luckily, everything is digital in the Digitown library:
- Each book has its parameters recorded: number of pages, weight.
- Each book has RFID sticker attached (RFID: radio-transmitter with ID).
- Each shelve in the Museum sends data: what RFIDs appear on the shelve and also measures actual total weight of books on the shelve.

Unfortunately, the RFID of the "De Revolutionibus Magnis Data" was found on the museum floor - detached and lonely.
Perhaps, you will be able to locate the book on one of the museum shelves and save the day?

PS: Don't hesitate to reach out for help and use Hints if you're feeling in trouble.

```kql
.execute database script <|
// Create table for the books
.create-merge table Books(rf_id:string, book_title:string, publish_date:long, author:string, language:string, number_of_pages:long, weight_gram:long)
// Import data for books
// (Used data is utilzing catalogue from https://github.com/internetarchive/openlibrary )
.ingest into table Books ('https://kustodetectiveagency.blob.core.windows.net/digitown-books/books.csv.gz') with (ignoreFirstRecord=true)
// Create table for the shelves
.create-merge table Shelves (shelf:long, rf_ids:dynamic, total_weight:long) 
// Import data for shelves
.ingest into table Shelves ('https://kustodetectiveagency.blob.core.windows.net/digitown-books/shelves.csv.gz') with (ignoreFirstRecord=true)
```

Which shelf is the book on?

Answer: 4242