# Use environment aware, secure and hierarchical config

<br/><br/>

### One Paragraph Explainer

When dealing with configuration data, many things can just annoy and slow down:

1. setting all the keys using process environment variables becomes very tedious when in need to inject 100 keys (instead of just committing those in a config file), however when dealing with files only the DevOps admins cannot alter the behavior without changing the code. A reliable config solution must combine both configuration files + overrides from the process variables

2. when specifying all keys in a flat JSON, it becomes frustrating to find and modify entries when the list grows bigger. A hierarchical JSON file that is grouped into sections can overcome this issue + few config libraries allow to store the configuration in multiple files and take care to union all at runtime. See example below

3. storing sensitive information like DB password is obviously not recommended but no quick and handy solution exists for this challenge. Some configuration libraries allow to encrypt files, others encrypt those entries during GIT commits or simply don't store real values for those entries and specify the actual value during deployment via environment variables.

4. some advanced configuration scenarios demand to inject configuration values via command line (vargs) or sync configuration info via a centralized cache like Redis so multiple servers will use the same configuration data.

5. the application should fail as fast as possible and provide the immediate feedback if the required environment variables are not present at start-up, this can be achieved by using [convict](https://www.npmjs.com/package/convict) to validate the configuration.

Some configuration libraries can provide most of these features for free, have a look at npm libraries like [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf), [config](https://www.npmjs.com/package/config), and [convict](https://www.npmjs.com/package/convict) which tick many of these requirements.

<br/><br/>

### Code Example – hierarchical config helps to find entries and maintain huge config files

```json5
{
  // Customer module configs 
  "Customer": {
    "dbConfig": {
      "host": "localhost",
      "port": 5984,
      "dbName": "customers"
    },
    "credit": {
      "initialLimit": 100,
      // Set low for development 
      "initialDays": 1
    }
  }
}
```

<br/><br/>
