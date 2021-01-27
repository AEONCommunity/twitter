# twitter

All things related to @aeoncommunity
This repository can be used to discuss things related to @aeoncommunity like making posts under the account. 

## How it works

`twitter-together` is using two workflows

1. `push` event to publish new tweets
2. `pull_request` event to validate and preview new tweets

### The `push` event

When triggered by the `push` event, the script looks for added `*.tweet` files in the `tweets/` folder or subfolders. If there are any, a tweet for each added tweet file is published.

If there is no `tweets/` subfolder, the script opens a pull request creating the folder with further instructions.

### The `pull_request` event

For the `pull_request` event, the script handles only `opened` and `synchronize` actions. It looks for new `*.tweet` files in the `tweets/` folder or subfolders. If there are any, the length of each tweet is validated. If one is too long, a failed check run with an explanation is created. If all tweets are valid, a check run with a preview of all tweets is created.
