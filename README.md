# ReversingLabsSDK
- [ReversingLabsSDK](#reversinglabssdk)
  * [Module: a1000](#module-a10000)
      - [Class A1000](#class)
      - [Parameters](#parameters)
      - [Methods](#class-methods)
  * [Module: ticloud](#module-ticloud)
      - [Common Parameters](#parameters-1)
      - [Class FileReputation](#class-1)
      - [Class AVScanners](#class-2)
      - [Class FileAnalysis](#class-3)
      - [Class RHA1FunctionalSimilarity](#class-4)
      - [Class RHA1Analytics](#class-5)
      - [Class URIStatistics](#class-6)
      - [Class URIIndex](#class-7)
      - [Class AdvancedSearch](#class-8)
      - [Class ExpressionSearch](#class-9)
      - [Class FileDownload](#class-10)
      - [Class URLThreatIntelligence](#class-11)
      - [Class AnalyzeURL](#class-12)
  * [Module: tiscale](#module-tiscale)
      - [Class TitaniumScale](#class-13)
      - [Parameters](#parameters-2)
      - [Methods](#methods-12)


![ReversingLabs](logo.jpg)


A Python SDK for ReversingLabs REST services (TitaniumCloud and appliances) - Python 2 version.

The idea behind this SDK is to enable easier out-of-the-box development of software integrations and automation services that need to interact with ReversingLabs.

The SDK consists of several modules, where each module represents one ReversingLabs service or ReversingLabs TitaniumCloud. 
 

***


## Module: a1000
A Python module representing the ReversingLabs A1000 malware analysis platform.
#### Class:
```python
class A1000(object)
def __init__(self, host, username=None, password=None, token=None, fields=__FIELDS, wait_time_seconds=2, retries=10, verify=True, proxies=None, user_agent=DEFAULT_USER_AGENT):
```

#### Parameters:
`host` - A1000 address  
`username` - A1000 username  
`password` - A1000 password  
`token` - A1000 user token for the REST API  
`fields` - optional fields that will be returned in the analysis report  
`wait_time_seconds` - wait time between each report fetching retry  
`retries` - number of report fetching retries  
`verify` - verify SSL certificate  
`proxies` - optional proxies in use  
`user_agent` - optional user agent string  

> *NOTE!*  
The default means of authorization on the ReversingLabs A1000 REST API is the token.  
If username and password are used instead, a token fetching request will be done so the token can be used in further actions without the user explicitly providing the token. 

#### Class methods:
- `configuration_dump`
    - Returns the configuration of the instantiated A1000 object
- `upload_sample_from_path`
    - Accepts a file path string and returns a response containing the analysis task ID
- `upload_sample_from_file`
    - Accepts a file open in 'rb' mode and returns a response containing the analysis task ID
- `get_results`
    - Accepts a list of hashes and returns a summary JSON report for each of them
    - This method utilizes the set number of retries and wait time in seconds to time
        out if the analysis results are not ready
- `upload_sample_and_get_results`
    - Accepts a file path string or an opened file in 'rb' mode for file upload and returns an analysis report response
    - This method combines uploading a sample and obtaining the analysis results
    - The result fetching action of this method utilizes the set number of retries and wait time in seconds to time
        out if the analysis results are not ready
- `get_classification`
    - Accepts one or more sample hashes and returns their classification
- `get_extracted_files`
    - Accepts a sample hash and returns a list of all files TitaniumCore engine extracted from the requested sample during static analysis
- `advanced_search`
    - Accepts a search query string and performs advanced search for local samples on A1000
    - Returns only one defined page of results using one request
- `advanced_search_aggregated`
    - Accepts a search query string and performs advanced search for local samples on A1000
    - Returns a list of results aggregated through multiple paginated requests
  

***


## Module: ticloud
A Python module representing the ReversingLabs TitaniumCloud API-s.

Each class in this module represents one TitaniumCloud API and can be instantiated using the same set of parameters:
```python
def __init__(self, host, username, password, verify=True, proxies=None, user_agent=DEFAULT_USER_AGENT, allow_none_return=False)
```
#### Parameters:
`host` - TitaniumCloud address  
`username` - TitaniumCloud username  
`password` - TitaniumCloud password  
`verify` - verify SSL certificate  
`proxies` - optional proxies in use  
`user_agent` - optional user agent string  
`allow_none_return` - if set to `True`, `404` response codes will return `None` instead of `NotFoundError`


#### Class:
```python
class FileReputation(TiCloudAPI)
```
#### Methods:
- `get_file_reputation`
    - Accepts a hash string or a list of hash strings and returns file reputation
    - Hash strings in a passed list must all be of the same hashing algorithm


#### Class:
```python
class AVScanners(TiCloudAPI)
```
#### Methods:
- `get_scan_results`
    - Accepts a hash string or a list of hash strings and returns AV scanner results
    - Hash strings in a passed list must all be of the same hashing algorithm


#### Class:
```python
class FileAnalysis(TiCloudAPI)
```
#### Methods:
- `get_analysis_results`
    - Accepts a hash string or a list of hash strings and returns extended file analysis
- `extract_uri_list_from_report`
    - Accepts a list of entries from the FileAnalysis report and returns a list of URI-s from those entries.
- `get_file_type`
    - Accepts a sample hash and returns the file type string


#### Class:
```python
class RHA1FunctionalSimilarity(TiCloudAPI)
```
#### Methods:
- `get_similar_hashes`
    - Accepts a hash string and returns a list of functionally similar hashes
    - Returns only one defined page of results using one request
- `get_similar_hashes_aggregated`
    - Accepts a hash string and returns a list of functionally similar hashes
    - Returns a list of results aggregated through multiple paginated requests


#### Class:
```python
class RHA1Analytics(TiCloudAPI)
```
#### Methods:
- `get_rha1_analytics`
    - Accepts one or more hash strings and returns a count of functionally similar hashes grouped by classification


#### Class:
```python
class URIStatistics(TiCloudAPI)
````
#### Methods:
- `get_uri_statistics`
    - Accepts a URI string and returns a count of files associated with that URI grouped by classification


#### Class:
```python
class URIIndex(TiCloudAPI)
````
#### Methods:
- `get_uri_index`
    - Accepts a URI string and returns a list of files associated with this URI
    - Returns only one defined page of results using one request
- `get_uri_index_aggregated`
    - Accepts a URI string and returns a list of files associated with this URI
    - Returns a list of results aggregated through multiple paginated requests


#### Class:
```python
class AdvancedSearch(TiCloudAPI)
````
#### Methods:
- `search`
    - Accepts a search query string and performs advanced search on the API
    - Returns only one defined page of results using one request
- `search_aggregated`
    - Accepts a search query string and performs advanced search on the API
    - Returns a list of results aggregated through multiple paginated requests


#### Class:
```python
class ExpressionSearch(TiCloudAPI)
````
#### Methods:
- `search`
    - Accepts a list containing the search query and performs expression search on the API
    - Returns only one defined page of results using one request
- `search_aggregated`
    - Accepts a list containing the search query and performs expression search on the API
    - Returns a list of results aggregated through multiple paginated requests
    
    
#### Class:
```python
class FileDownload(TiCloudAPI)
````
#### Methods:
- `get_download_status`
    - Accepts a hash string and returns the sample's availability for download
- `download_sample`
    - Accepts a hash string and downloads the related sample from TitaniumCloud
    
#### Class:
```python
class URLThreatIntelligence(TiCloudAPI)
````
#### Methods:
- `get_url_report`
    - Accepts a URL string and returns detailed URL analysis info
- `get_downloaded_files`
    - Accepts a URL string and returns a list of files downloaded from that URL
- `get_latest_url_analysis_feed`
    - Returns the latest URL analysis reports
    - Returns only one defined page of results using one request
- `get_latest_url_analysis_feed_aggregated`
    - Returns the latest URL analysis reports
    - Returns a list of results aggregated through multiple paginated requests
- `get_url_analysis_feed_from_date`
    - Accepts time format and a start time and returns URL analysis reports from that defined time onward
    - Returns only one defined page of results using one request
- `get_url_analysis_feed_from_date_aggregated`
    - Accepts time format and a start time and returns URL analysis reports from that defined time onward
    - Returns a list of results aggregated through multiple paginated requests

#### Class:
```python
class AnalyzeURL(TiCloudAPI)
````
#### Methods:
- `submit_url`
    - Sends a URL string for analysis and returns an analysis task ID


***

## Module: tiscale
A Python module representing the ReversingLabs TitaniumScale malware analysis appliance.
#### Class:
```python
class TitaniumScale(object)
def __init__(self, host, token, wait_time_seconds=2, retries=10, verify=True, proxies=None, user_agent=DEFAULT_USER_AGENT)
```
#### Parameters:
`host` - TitaniumScale address  
`token` - A1000 user token for the REST API  
`wait_time_seconds` - wait time between each report fetching retry  
`retries` - number of report fetching retries  
`verify` - verify SSL certificate  
`proxies` - optional proxies in use  
`user_agent` - optional user agent string  

#### Methods:
- `upload_sample_from_path`
    - Accepts a file path string for file upload and returns a response containing the analysis task URL
- `upload_sample_from_file`
    - Accepts a file opened in 'rb' mode for file upload and returns a response containing the analysis task URL
- `get_results`
    - Accepts an analysis task URL and returns a file analysis summary or a full analysis report
    - This method utilizes the set number of retries and wait time in seconds to time out if the analysis results are not ready
- `upload_sample_and_get_results`
    - Accepts a file path string or an opened file in 'rb' mode for file upload and returns a file analysis summary or a full analysis report
    - This method combines uploading a sample and obtaining the analysis results
    - The result obtaining action of this method utilizes the set number of retries and wait time in seconds to time out if the analysis results are not ready

