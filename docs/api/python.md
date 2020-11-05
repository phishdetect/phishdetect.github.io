# Python API

PhishDetect Node's REST API is also easily accessible through an MIT licensed [Python 3 library](https://github.com/phishdetect/phishdetect-python) which can be simply installed (and updated) with:

```bash
pip3 install -U phishdetect
```

Once installed, you can instantiate a connection to your PhishDetect Node like following:

```python
import phishdetect

# You have to specify the base host of your PhishDetect Node (including the
# schema). The API key is optional, although it is required by some admin-level
# APIs.
pd = phishdetect.PhishDetect(host="https://your-server.com",
                             api_key="your-api-key")
```

You can now use the `pd` object to access all PhishDetect Node's API routes. All available models are detailed in the reference below, and are accessible from an instantiated `PhishDetect` object. If you are looking for some practical examples, you can have a look at the collection of utilities built using this Python API available [here](http://github.com/phishdetect/phishdetect-utils).

---

::: phishdetect.models.users

::: phishdetect.models.indicators

::: phishdetect.models.alerts

::: phishdetect.models.reports

::: phishdetect.models.analyze
