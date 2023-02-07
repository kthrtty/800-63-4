---
layout: default.ja
title: Strength of Memorized Secrets
navOrder: 13
navTitle: Secrets
permalink: /sp800-63b/secrets/
anchor: appA
section: A
---

# Strength of Memorized Secrets {#appA}

*This appendix is informative.*

<!--
Throughout this appendix, the word "password" is used for ease of discussion. Where used, it should be interpreted to include passphrases and PINs as well as passwords.
-->

本 Appendix を通じて, 議論を容易にするため "Password" という用語を用いる.
本用語が用いられる箇所では, Password に加え Passphrase や PIN も含むと解釈すべきである.

## Introduction

<!--
Despite widespread frustration with the use of passwords from both a usability and security standpoint, they remain a very widely used form of authentication [[Persistence]](references.md#ref-persistence). Humans, however, have only a limited ability to memorize complex, arbitrary secrets, so they often choose passwords that can be easily guessed. To address the resultant security concerns, online services have introduced rules in an effort to increase the complexity of these memorized secrets. The most notable form of these is composition rules, which require the user to choose passwords constructed using a mix of character types, such as at least one digit, uppercase letter, and symbol. However, analyses of breached password databases reveal that the benefit of such rules is not nearly as significant as initially thought [[Policies]](references.md#ref-policies), although the impact on usability and memorability is severe.
-->

Usability とセキュリティ双方の観点で Password の使用に関するフラストレーションが広がっているが, Password は依然として広く Authentication に使われている方式である [[Persistence]](references.md#ref-persistence).
しかしながら, 人間は複雑で勝手に決められたシークレットを記憶する能力が限られており, しばしば簡単に推測可能な Password を選択することになる.
この結果生じるセキュリティ上の懸念に対応するため, オンラインサービスは Memorized Secret の複雑度を上げるようなルールを導入してきた.
最も顕著なルール形式はその構成ルールであり, 1つ以上の数字, 大文字および記号など, 複数の文字種を用いることをユーザーに要求するようなものである.
しかしながら, 侵害された Password データベースの分析からは, そのようなルールがもたらす Usability への影響や記憶しづらさのわりに, それによる恩恵は当初考えられていたほど大したものではないことが明らかになっている [[Policies]](references.md#ref-policies).

<!--
Complexity of user-chosen passwords has often been characterized using the information theory concept of entropy [[Shannon]](references.md#ref-shannon). While entropy can be readily calculated for data having deterministic distribution functions, estimating the entropy for user-chosen passwords is difficult and past efforts to do so have not been particularly accurate. For this reason, a different and somewhat simpler approach, based primarily on password length, is presented herein.
-->

ユーザー選択により生成された Password の複雑度は, しばしば Entropy という情報理論のコンセプトを使って特徴づけられることがある [[Shannon]](references.md#ref-shannon).
決定論的分布関数を持つデータの Entropy は容易に計算可能だが, ユーザー選択の Password の Entropy を推定するのは困難であり, そのための過去の努力はあまり正確ではなかった.
そのため, それとは異なりよりシンプルなアプローチとして, 主に Password の長さに基づくものをここに示す.

<!--
Many attacks associated with the use of passwords are not affected by password complexity and length. Keystroke logging, phishing, and social engineering attacks are equally effective on lengthy, complex passwords as simple ones. These attacks are outside the scope of this Appendix.
-->

Password の使用に関連する Attack の多くは, Password の複雑性と長さには影響されない.
キーストロークロギング, Phishing および Social Engineering Attack は, シンプルな Password に対して有効であるのと同様に, 長く複雑な Password に対しても有効である.
こういった Attack は本 Appendix のスコープ外とする.

## Length

<!--
Password length has been found to be a primary factor in characterizing password strength [[Strength]](references.md#ref-strength) [[Composition]](references.md#ref-composition). Passwords that are too short yield to brute force attacks as well as to dictionary attacks using words and commonly chosen passwords.
-->

Password の長さは Password 強度を特徴づける第一のファクターであることがわかっている [[Strength]](references.md#ref-strength) [[Composition]](references.md#ref-composition).
短すぎる Password は, 単語や一般的に使用される Password を用いた辞書攻撃や Brute Force Attack の対象となる.

<!--
The minimum password length that should be required depends to a large extent on the threat model being addressed. Online attacks where the attacker attempts to log in by guessing the password can be mitigated by limiting the rate of login attempts permitted. In order to prevent an attacker (or a persistent claimant with poor typing skills) from easily inflicting a denial-of-service attack on the subscriber by making many incorrect guesses, passwords need to be complex enough that rate limiting does not occur after a modest number of erroneous attempts, but does occur before there is a significant chance of a successful guess.
-->

最低限必要な Password の長さは, 対応する脅威モデルに大きく依存する.
Attacker が Password を推測してログインを試みる Online Attack は, 許容するログイン試行回数を制限することで軽減可能である.
Attacker (またはタイピングスキルの低い執拗な Claimant) が大量の誤推測により Subscriber に対して Denial-of-Service Attack を引き起こすのを防ぐため, Password は十分複雑で, 適度な入力回数ではレートリミットに到達しないが, 推測が成功する可能性がかなり高くなる前にはレートリミットに到達するようなものとする必要がある.

<!--
Offline attacks are sometimes possible when one or more hashed passwords is obtained by the attacker through a database breach. The ability of the attacker to determine one or more users' passwords depends on the way in which the password is stored. Commonly, passwords are salted with a random value and hashed, preferably using a computationally expensive algorithm. Even with such measures, the current ability of attackers to compute many billions of hashes per second with no rate limiting requires passwords intended to resist such attacks to be orders of magnitude more complex than those that are expected to resist only online attacks.
-->

Attacker がデータベース侵害を通じて1つ以上のハッシュ化された Password を取得すると, Offline Attack が可能になることもある.
Attacker が1人以上のユーザーの Password を特定できるかは, Password の保存方法に依存する.
通常 Password は乱数値の Salt を用いてハッシュ化されており, さらに計算コストの高いアルゴリズムが使用されていればなお良い.
そのような対策を講じても, 現在の Attacker はレートリミットなしで毎秒数十億のハッシュ計算が可能であり, そのような攻撃に対抗できる Password は Online Attack に抵抗できると予想される Password より桁違いに複雑でなければならない.

<!--
Users should be encouraged to make their passwords as lengthy as they want, within reason. Since the size of a hashed password is independent of its length, there is no reason not to permit the use of lengthy passwords (or pass phrases) if the user wishes. Extremely long passwords (perhaps megabytes in length) could conceivably require excessive processing time to hash, so it is reasonable to have some limit.
-->

ユーザーには, 合理的な範囲内で Password を好きなだけ長くすることを推奨するべきである.
ハッシュ化された Password のサイズは元の Password の長さとは無関係であるため, ユーザーが希望しているのに長い Password (ないし Passphrase) の利用を許可しない理由はない.
非常に長いパスワード (おそらくメガバイト級) はハッシュ化に過度の処理時間を要する可能性があるため, そういった制限を設けるのは合理的である.

## Complexity

<!--
As noted above, composition rules are commonly used in an attempt to increase the difficulty of guessing user-chosen passwords. Research has shown, however, that users respond in very predictable ways to the requirements imposed by composition rules [[Policies]](references.md#ref-policies). For example, a user that might have chosen "password" as their password would be relatively likely to choose "Password1" if required to include an uppercase letter and a number, or "Password1!" if a symbol is also required.
-->

上述のように, 構成ルールは, ユーザー選択による Password の推測を困難にするために一般的に利用されている.
しかし, 調査によると, ユーザーは構成ルールで課される要件に対して非常に推測容易な方法で応答することが示されている [[Policies]](references.md#ref-policies).
例えば, Password として "password" を選択しようとするユーザーは, 大文字と数字を含める必要がある場合には "Password1" を, 記号も必要な場合は "Password1!" を選択する可能性が比較的高い.

<!--
Users also express frustration when attempts to create complex passwords are rejected by online services. Many services reject passwords with spaces and various special characters. In some cases, the special characters that are not accepted might be an effort to avoid attacks like SQL injection that depend on those characters. But a properly hashed password would not be sent intact to a database in any case, so such precautions are unnecessary. Users should also be able to include space characters to allow the use of phrases. Spaces themselves, however, add little to the complexity of passwords and may introduce usability issues (e.g., the undetected use of two spaces rather than one), so it may be beneficial to remove repeated spaces in typed passwords prior to verification.
-->

また, 複雑な Password を生成しようとしてオンラインサービスに拒否されると, ユーザーはフラストレーションを感じる.
多くのサービスは, スペースやさまざまな特殊文字を含む Password を拒否する.
場合によっては, 受け入れられない特殊文字は, そういった文字に依存する SQL インジェクションなどの Attack を回避するためな可能性もある.
しかしながら, 適切にハッシュ化された Password はどのような場合でもデータベースにそのまま送られるわけではないため, そのような予防策は不要である.
さらに, ユーザーがフレーズを使用できるよう, スペースを含められるようにもすべきである.
ただし, スペース自体は Password の複雑さをほとんど増やすこともなく, Usability の問題 (e.g., 気づかずに1つではなく2つのスペースを入力してしまう) を引き起こす可能性もあるため, 入力 Passsword 中の連続するスペースを Verification 前に取り除くことが有益な場合もある.

<!--
Users' password choices are very predictable, so attackers are likely to guess passwords that have been successful in the past. These include dictionary words and passwords from previous breaches, such as the "Password1!" example above. For this reason, it is recommended that passwords chosen by users be compared against a blocklist of unacceptable passwords. This list should include passwords from previous breach corpuses, dictionary words, and specific words (such as the name of the service itself) that users are likely to choose. Since user choice of passwords will also be governed by a minimum length requirement, this dictionary need only include entries meeting that requirement. As noted in [Sec. 5.1.1.2](sec5_authenticators.md#memsecretver), it is not beneficial for the blocklist to be excessively large or comprehensive, since its primary purpose is to prevent the use of very common passwords that might be guessed in an online attack before throttling restrictions take effect. An excessively large blocklist is likely to frustrate users that attempt to choose a memorable password.
-->

ユーザーの Password 選択は非常に予測しやすいため, Attacker は過去に利用に成功したものをもとに Password を推測する可能性がある.
これには, 上記例の "Password1!" のような, 過去に侵害された辞書単語や Password を含む.
そのため, ユーザー選択の Password を受け入れ不可な Password の Blocklist と比較することを推奨する.
このリストには, 過去に侵害された事例で用いられた Password, 辞書単語やユーザーが選択しがちな特定単語 (サービス自体の名前など) から生成された Password を含めるべきである.
ユーザー選択の Password も最小長要件に従うため, この辞書にはそのような要件にあったエントリーのみを含める必要がある.
[Sec. 5.1.1.2](sec5_authenticators.md#memsecretver) で述べたように, Blocklist があまりに大きく包括的であることは有益ではない.
Blocklist の主な目的は, Online Attack で Throttling 制限に到達するまでに推測されてしまう可能性のある非常に一般的な Password の利用を防ぐことである.
Blocklist が大きすぎると, 覚えやすい Password を選択しようとするユーザーにフラストレーションを与えかねない.

<!--
Highly complex memorized secrets introduce a new potential vulnerability: they are less likely to be memorable, and it is more likely that they will be written down or stored electronically in an unsafe manner. While these practices are not necessarily vulnerable, statistically some methods of recording such secrets will be. This is an additional motivation not to require excessively long or complex memorized secrets.
-->

非常に複雑な Memorized Secret は新たな潜在的脆弱性をもたらす.
そういった Memorized Secret は記憶に残る可能性が低く, 安全でない方法で書き留められたり電子的に保存される可能性が高い.
そういった慣行が必ずしも脆弱であるわけではないが, 統計的にはそういったシークレットの記録方法はのいくらかは脆弱になりがちである.
これは過度に長く複雑な Memorized Secret を要求しないという追加のモチベーションとなる.

## Central vs. Local Verification

<!--
While passwords that are used as a separate authentication factor are generally verified centrally by the CSP's verifier, those that are used as an activation factor for a multi-factor authenticator are either verified locally or are used to derive the authenticator output, which will be incorrect if the wrong activation factor is used. Both of these situations are referred to as "local verification".
-->

単体の Authentication Factor として利用される Password は, 通常 CSP の Verifier によって中央で一元的に検証されるが, Multi-factor Authenticator の Activation Factor として利用される Password は, ローカルで検証されたり Authenticator Output の導出 (Activation Factor が正しくなければ Authenticator Output も正しくならない) のために用いられる.
こういったシチュエーションは "Local Verification" と呼ばれる.

<!--
The attack surface and vulnerabilities for central and local verification are very different from each other. Accordingly, the requirements for memorized secrets verified centrally is different from those verified locally. Centrally verified secrets require the verifier, which is an online resource, to store salted and iteratively hashed verification secrets for all subscribers' passwords. Although the salting and hashing process increases the computational effort to determine the passwords from the hashes, the verifier is an attractive target for attackers, particularly those who are interested in compromising an arbitrary subscriber rather than a specific one.
-->

Central Verification と Local Verification の Attack 対象領域と脆弱性は互いに大きく異なる.
したがって, 中央で検証される Memorized Secret に対する要件とローカルで検証されるそれは異なる.
中央で検証されるシークレットには, オンラインリソースである Verifier が, 全ての Subscriber の Password に対して Salt 付きで繰り返しハッシュ化した Verification シークレットを保存する必要がある.
Salt およびハッシュ化プロセスはハッシュ値から Password を特定するための計算量を増大させるが, Verifier は Attacker にとっての格好の標的となる. 特定の Subscriber ではなく任意の Subscriber を侵害することに関心を持つ Attacker であればなおさらである.

<!--
Local verifiers do not have the same concerns with attacks at scale on a central online verifier, but depend to a greater extent on the physical security of the authenticator and the integrity of its associated endpoint. To the extent that the authenticator stores the activation factor, that factor must be protected against physical and side-channel (e.g., power and timing analysis) attacks on the authenticator. When the activation factor is entered through the associated endpoint, the endpoint needs to be free of malware, such as key-logging software, if the password is to be protected. Since these threats are less dependant on the length and complexity of the password, those requirements are relaxed for local verification.
-->

ローカルの Verifier には, 中央のオンラインな Verifier に対する大規模攻撃のような心配はないが, Authenticator の物理セキュリティと関連するエンドポイントの Integrity (完全性) により大きく依存する.
Authenticator が Activation Factor を保存する範囲で, その Activation Factor は物理攻撃および Side-Channel Attack (e.g., 電力およびタイミング解析) から保護しなければならない.
関連するエンドポイントから Activation Factor が入力される際は, そのエンドポイントがマルウェアに感染していてはならない.
例えば Password を保護する場合は, キーロガーソフトウェアなどが防ぐべきマルウェアになる.
これらの脅威は Password の長さと複雑さにあまり依存しないため, こういった要件は Local Verification では緩和される.

<!--
Online password-guessing attacks are a similar threat for centrally and locally verified passwords. Throttling, which is the primary defense against online attacks, can be particularly challenging for local verifiers because of the limited ability of some authenticators to securely store information about unsuccessful attempts. Throttling can be performed by either keeping a count of invalid attempts in the authenticator, or by generating an authenticator output that is rejected by the CSP verifier, which does the throttling. In this case it is important that the invalid outputs not be obvious to the attacker, who could otherwise make offline attempts until a valid-looking output appears.
-->

Online Password-guessing Attack は, 中央およびローカルで検証される Password ともに共通した脅威である.
Online Attack に対する主要な防御策である Throttling は, ローカルの Verifier にとっては特に困難となる可能性がある.
そういった Authenticator の中には, 失敗試行に関する情報をセキュアに保存する能力が限られているものもある.
Throttling は, Authenticator 内に無効な試行の回数を保持するか, Throttling を行う CSP Verifier に拒否されるような Authenticator Output を生成することで実現できる.
この場合, Authenticator Output が無効であることが Attacker に明らかにならないことが重要である.
さもないと Attacker は有効に見える Authenticator Output が出力されるまでオフライン試行を繰り返すことができる.

## Summary

<!--
Length and complexity requirements beyond those recommended here significantly increase the difficulty of memorized secrets and increase user frustration. As a result, users often work around these restrictions in a way that is counterproductive. Furthermore, other mitigations such as blocklists, secure hashed storage, and rate limiting are more effective at preventing modern brute-force attacks. Therefore, no additional complexity requirements are imposed.
-->

ここで推奨されている以上の長さと複雑さの要件は, Memorized Secret の難易度を大幅に高め, ユーザーのフラストレーションを増加させる.
その結果, ユーザーはしばしばそういった制約の回避策として逆効果な方法を選ぶこともある.
さらに, Blocklist, セキュアでハッシュ化されたストレージ, レートリミットなどのその他の軽減策は, モダンな Brute-force Attack を防ぐのにより効果的である.
したがって, 追加の複雑さの要件は課さない.
