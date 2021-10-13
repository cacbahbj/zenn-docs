---
title: "GitHubとSlackを連携する"
emoji: "😎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["github", "slack"]
published: true
---
GitHubとSlackの連携は以下の3つのやり方があります
使用するAppは同じですが設定する場所や方法が違います

リアルタイムもしくはリマインダー通知を設定できますが、以下の注意書きがあります
> GitHubは、オーナーごとに5つのリポジトリまで、リポジトリごとに20のPull Requestまでしかリマインダーをトリガーしません。

# アクティビティをリアルタイムで指定したチャンネルに通知する

GitHubにコミットした、などのタイミングで指定したチャンネルに通知を行う方法です
Slack用のアプリをインストールしたあと、チャンネルで「/github」のスラッシュコマンドで設定します

https://slack.com/intl/ja-jp/help/articles/232289568-GitHub-と-Slack-を連携させる

通知のカスタマイズは以下に詳しく書いてあります
（コメントやブランチ操作なども通知したい場合など）

https://github.com/integrations/slack#configuration

ちなみに、スラッシュコマンドではチケットのクローズなどもできます

# チャンネルにリマインダー通知する

こちらは指定した時間に指定したチャンネルへリマインダー通知する方法です
GithubのOrganizationやTeamのSetting->Scheduled remindersから設定します

https://docs.github.com/ja/organizations/managing-organization-settings/managing-scheduled-reminders-for-your-organization
https://docs.github.com/ja/organizations/organizing-members-into-teams/managing-scheduled-reminders-for-your-team

# SlackのAppで通知する

SlackのAppで個人宛に通知する方法で、リアルタイムとリマインダーの両方が設定できます
GitHubのプロフィール->Setting->Scheduled remindersから設定します

https://docs.github.com/ja/account-and-profile/setting-up-and-managing-your-github-user-account/managing-your-membership-in-organizations/managing-your-scheduled-reminders

チャンネルへのリマインダーと違い、通知するリポジトリが選択できなかったり
Draftでも通知されるなどの違いがあります

※その他にも設定できる項目に違いがあります
