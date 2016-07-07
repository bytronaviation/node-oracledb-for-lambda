# node-oracledb-for-lambda

This module is a fork of [node-oracledb](https://github.com/oracle/node-oracledb) v1.9.3, precompiled for AWS Lambda, Node.js 4.3.

The scripts to reproduce the build process can be found at [node-oracledb-lambda-test](https://github.com/nalbion/node-oracledb-lambda-test). 

# Usage

In addition to the usual package.json and *.js files, you also need to include the 
Oracle Instant Client libraries provided in `lambda-lib` - they should be in your zip file's `lib/` directory.

```bash
npm install --save oracledb-for-lambda

zip app.zip index.js package.js \
   your-other-dependencies... \
   node_modules/oracledb-for-lambda/package.json \
   node_modules/oracledb-for-lambda/index.js \
   node_modules/oracledb-for-lambda/lib/*.js \
   node_modules/oracledb-for-lambda/build/Release/oracledb.node \
   lib/*.so* \
```

Due to the size of the Oracle libraries, you will need to deploy your zip file to S3 and get Lambda to download from the S3 URL.

## Instant Client Light
Unless you require error messages in languages other than English, you will probably want to use the [Instant Client Light (English) version](https://docs.oracle.com/database/121/LNOCI/oci01int.htm#LNOCI13309).

**NOTE: This will significantly reduce the size of your zip and make deployment much easier**

```bash
# after npm install, and before creating your zip:
rm lib/ociei.so
```

If you do require the standard version, you can delete `libociicus.so`