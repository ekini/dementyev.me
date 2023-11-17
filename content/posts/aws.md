+++
title = "Your AWS account root credentials are not really safe"
date = "2023-11-17"
description = "MFA on AWS account can be silently bypassed without interacting with support"
tags = [
"aws",
"mfa"
]
+++

Root credentials are quite important to protect. So you usually choose a very strong password, add a hardware key as MFA and put it into a safe.

You think that's enough for the AWS account to be safe but it's actually not and the MFA can
be bypassed quite easily. Furthermore, AWS are saying this is the way it should work.

### The process

Obviously, it's not going to be very easy, but in real world all of the below is quite achievable.

The main prerequisite is to have read access to the mailbox the account is
registered too.

The second one is to have some kind of privileged access via an IAM user or an IAM role with appropriate permissions that allow you to change the phone in the account settings.

Here's how it works in 5 simple steps:

1. You change the phone number to any under your control.
2. You reset the root user password via email and get asked for MFA
3. Now click "Troubleshoot MFA" and choose "Sign in using alternative factors of authentication"
4. You'll get another link in the email and then get a call to the phone you just entered
5. The hardware key that was attached as MFA didn't mean anything and now you have full access to the AWS account and can do whatever you want with it.

### Thoughts

Here's why I think it shouldn't work like this.

It's quite possible that somebody gets read only access to your email. What if you forget to lock your computer and an attacker can perform the password reset procedure quickly. Or they can steal the session and install a proxy on your machine to have the same usual IP as you. Or if you use an insecure email provider, that can be hacked.

These things happen.

Secondly, getting IAM access is possible too. These days people run terraform in CI/CD pipelines and I'm pretty sure most of them use AdministratorAccess for that. Now your attack surface widens to "anyone who can push code" because now they can change that phone in the email.

Thirdly, MFA should mean something. What's the point of it if you can easily reset it offline? There should be some kind of cooldown before letting you into the account. Make it at least a couple of days.

And finally, changing the phone used to reset MFA for the root user shouldn't probably be changeable by IAM users/roles at all? At least there should be a call to the old phone to confirm the change and again, a cooldown.

And maybe this procedure should involve AWS support, however if anything goes wrong, it puts responsibility on them not the customer.

### Possible mitigations

Well, the first thing you should probably be doing is having a separate email account for the AWS account and not reuse it anywhere. Protect that with MFA and login only in rare cases when it's really required.

Then create an Organization and a bunch of subaccounts. Use Organization policies to disallow changing the account information from IAM no matter which privileges IAM users/roles have in the subaccounts. If you have IAM users or roles in that account, use permission boundaries to disallow changing account information.

If you have to use one account be very careful around granting roles, and again use permission boundaries.

