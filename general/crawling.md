# Crawling

## Summary

1. [Extracting Valuable information](#extracting-valuable-information)
2. [Scrapy](#scrapy)
3. [Create a Spider](#create-a-spider)
4. [Run the Spider](#run-the-spider)

## Extracting Valuable information

- **Links**: Extract links to other pages or resources.
- **Comments**: Comments sections on blogs, forums, or other interactive pages can be a goldmine of information. Users often inadvertently reveal sensitive details, internal processes, or hints of vulnerabilities in their comments.

- **Metadata**: Extract metadata from HTML tags, such as `<meta>`, `<title>`, and `<link>`, which can provide insights into the page's purpose and content.

- **Sensitive Files**: Look for links to sensitive files like `.env`, `.git`, or other configuration files that may contain credentials or sensitive information.s

## Scrapy

```bash

pip install scrapy

scrapy startproject mycrawler
cd mycrawler

```

### Create a Spider

```python
import scrapy

class ExampleSpider(scrapy.Spider):
    name = 'example'
    start_urls = ["https://example.com"]

    def parse(self, response):
        for link in response.css('a::attr(href)').getall():
            yield {'link': response.urljoin(link)}

        for next_page in response.css('a.next::attr(href)').getall():
            yield response.follow(next_page, self.parse)
```

### Run the Spider

```bash

scrapy crawl example -o links.json

```


