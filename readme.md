# Pulumi Remotion Lambda

Easy to deploy Remotion Lambda with Pulumi/SST in a few lines of code and after use that with a client.

## Usage 

```ts
const remotion = new RemotionLambda("Remotion", {
    path: "remotion-example",
    function: {
        ephemerealStorageInMb: 2048,
        memorySizeInMb: 2048,
        timeoutInSeconds: 120,
    },
});
new sst.aws.Astro("Client", {
    path: "client",
    environment: {
    REMOTION_FUNCTION_NAME: remotion.function.name,
    REMOTION_SITE_URL: remotion.siteUrl,
    REMOTION_BUCKET_NAME: remotion.bucket.bucket,
    },
});
```

## Todo
- make it possible to deploy multiple stacks (main, dev, etc) in the same account, currently setting the function, role and bucket name are hardcoded so you can't have the same name with different stacks
- custom domains for lambda, like SST does for every FE stack
- everything in bucket is public
- the first deploy fails rn bc bucket isn't ready yet, so you need to run deploy twice at first