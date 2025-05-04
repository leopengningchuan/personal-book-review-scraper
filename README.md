# Douban Book Scrapping
Parsing Personal Douban Book Reading

## Project Background
[Douban.com](https://www.douban.com) is a popular online platform and social network where users can discover, review, and share content related to films, books, music, events, and more. As an active user since 2012, I’ve written numerous reviews and articles about books and movies over the years. My experience with Douban has been both enriching and memorable.

However, Douban doesn’t offer a convenient way to export all user-generated content in one click. This raises concerns about data loss in the event of platform failure. To safeguard my reviews, I created a custom web parser to automatically extract and store all my book reviews locally. This ensures my content is securely backed up and easily accessible, regardless of the platform’s future.

## Project Goal
This project is focusing on using **Python Jupyter Notebook** to parsing the personal book reviews and comments in [Douban Book](https://book.douban.com).

## Table of Contents
- README.md
- LICENSE.txt
- Douban Book Scrapping.ipynb
- Douban_books_result.xlsx (sample data output)

## Instructions
### 1. Package Used
- `pandas, numpy, re, requests, math`: for data manipulation
- `BeautifulSoup`: for parsing from the website

### 2. Header Generated
To parse personal book data from Douban, you must be logged into your account. Instead of entering credentials manually, the program uses an HTTP header that mimics a logged-in session. This header includes two key components: your **User Agent** and **Login Cookie**.

- **User Agent**: This identifies your browser and operating system. Please refer to [What is my User Agent?](https://www.whatismybrowser.com/detect/what-is-my-user-agent/) for more information.
- **Login Cookie**: This simulates your logged-in session. To retrieve it:
  1. Open your browser and visit the [Douban Book Login](https://accounts.douban.com/passport/login) page.
  2. Open the **Developer Tools** (usually `F12` or right-click > "Inspect")
  3. Log in to your Douban account.
  4. In the **Network** tab of Developer Tools, find a request sent to Douban after login.
  5. Check the **Request Headers** to locate the `cookie` field — copy its full value.

You will also need your **Douban ID**, which is visible on your profile page (typically near your username or in the URL when viewing your profile).

### 3. Parse the Information
After generating the header, the Jupyter Notebook proceeds to parse the books listed in the user's personal Douban account. However, since the program doesn't initially know how many pages it needs to process, it first determines the total number of books recorded in the account.

#### 3.1: Determine Total Number of Pages
The program begins by reading the main book information page to extract the total count of books. Since each page typically contains 15 books, the total number of pages required for parsing is calculated as: `ceiling(total number of books / 15)`.

#### 3.2: Parse Book Details Page by Page
For each page, the program parses book information one by one, extracting the following details:

- **Name**: The title of the book
- **Pub_info**: Publishing information, including author, translator, publisher, price, etc.
- **Date**: The date the book was marked as "read"
- **Star**: User rating, from 1 to 5
- **Tag**: Tags used to describe or categorize the book
- **Comment**: User's written review or comment
- **Website**: The URL to the book’s Douban page

Each page's data is compiled into a dataset, which is then concatenated with datasets from the other pages to form a complete collection.

During this process, the program will display status updates such as:

>  Parsing books: n ~ m...

 This message indicates the current range of books being processed. If an error occurs during parsing, the program will raise a clear and informative reminder for the book which has not been successfully parsed.

#### 3.3: Completion
Once all books have been successfully parsed, the program will display the final message:

>  Finish parsing all books.

### 4. Clean and Export the data
Once all the data is parsed from the website, the next step is to perform basic data cleaning. After ensuring that all the data is properly cleaned and formatted, an Excel file will be generated containing the complete dataset.

## License
This project is licensed under the MIT License - see the [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) file for details.

## Acknowledgements
- Thanks to [`BeautifulSoup`](https://www.crummy.com/software/BeautifulSoup/) for web scraping.
- Thanks to [Douban](https://www.douban.com) for providing the platform.
