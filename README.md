# twitter

All things related to @aeoncommunity
This repository can be used to discuss things related to @aeoncommunity like making posts under the account. 

# The tweets/ folder

To create a new tweet create a new `*.tweet` file in this `tweets/` folder.

<kbd>[Create new tweet](../../../new/master/?filename=tweets/<your-path>.tweet)</kbd>

## Example

Create a new file `tweets/hello-world.tweet` with the content

> Hello, world!

You can use subfolders, e.g. `tweets/2019-02/hello-world.tweet`, as long as the file is in the `tweets/` folder and has the `.tweet` file extension

## Create a tweet with a twitter poll

**Note**: The configured twitter account needs to be authorized to use Twitters Ads API in order to send tweets including a poll.

A tweet including a poll must end with 2-4 options in the following format

> Here is some text
>
> ( ) option A  
> ( ) option B  
> ( ) option C  
> ( ) option D

## Notes

- Only newly created files are handled, deletions, updates or renames are ignored.
- `*.tweet` files will not be created for tweets you send out directly from twitter.com
- If you need to rename an existing tweet file, please do so locally using [`git mv old_filename new_filename`](https://help.github.com/en/articles/renaming-a-file-using-the-command-line), otherwise it may occur as deleted and added which would trigger a new tweet.
- your message must fit into a single tweet

## How it works

`twitter-together` is using two workflows

1. `push` event to publish new tweets
2. `pull_request` event to validate and preview new tweets

### The `push` event

When triggered by the `push` event, the script looks for added `*.tweet` files in the `tweets/` folder or subfolders. If there are any, a tweet for each added tweet file is published.

If there is no `tweets/` subfolder, the script opens a pull request creating the folder with further instructions.

### The `pull_request` event

For the `pull_request` event, the script handles only `opened` and `synchronize` actions. It looks for new `*.tweet` files in the `tweets/` folder or subfolders. If there are any, the length of each tweet is validated. If one is too long, a failed check run with an explanation is created. If all tweets are valid, a check run with a preview of all tweets is created.
