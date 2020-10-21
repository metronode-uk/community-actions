# AutoPunishments
*Yup, you read that correctly.*

---
This action overwrites the default `a!warn` command to enable automated punishments being taken on a user depending on how many warns they have. The command still functions exactly as it should and only changes functionality on the `add` subcommand or if you're using `a!warn @User` directly - none of these changes are outwardly noticeable though (except when a punishment is given).

By default:

| When you have this many warnings... | This will happen |
|-------------------------------------|------------------|
| 1 warning                           | Kick             |
| 2 warnings                          | 1 day mute       |
| 3 warnings                          | 3 day tempban    |
| 4 warnings                          | Permanent ban    |

The action is fully configurable - you can change what action you want to take and you can change the options that are added to the punishment (duration, reason, etc)

## Setup
1. To set this action up, **create a new role** in your server. Doesn't matter what you name it, but **make sure it is at the bottom of the role list**. Grab the ID of the role (you can use `a!id` or Development Mode if you have it enabled) and save it for later.
2. Next, import the action into your server using the [instructions on the main CAR page](https://github.com/atlasbot/community-actions#import-actions-from-this-repository-into-your-server).
3. Put the ID you wrote down into the very top line of the action, replacing all of the `00000`s there
4. (Optional) Edit the `punishment_tier_#__` variables however you want.
    - `minwarnings` is how many warnings the user should have for this action to be taken.
    - `punishment` is the punishment to carry out when the user reaches however many warnings set in that tier's `minwarnings`. Accepted values are `kick`, `mute`, `tempban`, `ban`. Any other value will result in nothing happening - so feel free to leave it empty or fill it with gibberish to make nothing happen.
    - `opts` is the options for that tier. This value only really applies to `mute` or `tempban` punishments - for these, `opts` acts as the duration to mute/tempban the user for.
5. ???
6. Profit.

## How does it work?
Being a savvy and elite programmer *(read: idiot)* I added the `{user.infractions}` tag to Atlas v8. This tag accepts an argument for a user, and will return the number of infractions a user has in your server.

I literally only created that tag so I could create this action. How's that for a flex?

## Disclaimers
- Because of the way that Actions work, users can only carry out the punishments for a specific tier if they have the permission to execute that punishment's command. i.e, if a moderator can't `a!ban` someone, this action will not ban a user when they are warned by that moderator, even if they are on that punishment's tier.
- For some reason, `{user.infractions}` will only return a value **if the user is in the server**. This means that, if the user is not in the server, they can still be warned but they will not receive any sort of punishment. So if that user is on a tier where they would normally be banned, they won't be and you'll have to ban them manually. It's a bit of a drawback but there's nothing I can do about it and Sylver won't help me fix it. So if you want it fixed, shout at him.

## Special Thanks
- Myself for creating `{user.infractions}` and then procrastinating creating this action