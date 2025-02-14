---
layout: default.ja
title: Federation Assurance Level
navOrder: 4
navTitle: FAL
permalink: /sp800-63c/fal/
anchor: fal
section: 4
---

# Federation Assurance Level (FAL) {#fal}

*This section is normative.*

<!--
This section defines allowable *federation assurance levels* (FALs). The FAL describes requirements for securing federation transactions, including requirements on how relationships between IdPs and RPs are established and how assertions are presented and protected. These levels can be requested by an RP at runtime or required by the configuration of both the RP and the IdP for a given transaction. The FAL provides assurances for the RP receiving the assertion as well as assurances for the IdP creating the assertion to be used by an RP.
-->

本セクションでは, *Federation Assurance Level (FAL)* を規定する.
FAL は Federation Transaction に関するセキュリティ要件を定める. これには IdP と RP の関係確立方法や Assertion の提示・保護方法に関する要件を含む.
このレベルは RP がランタイム毎に要求することもあり, RP と IdP が所与の Transaction に対して事前に設定することもある.
FAL は, RP が Assertion を受け取る際の確度を示すとともに, IdP が RP に利用される Assertion を生成する際の確度を示す.

<!--
While many different federation implementation options are possible, the FAL is intended to provide clear guidance representing increasingly secure deployment options. See [[SP800-63]](../_sp800-63/sec1_purpose.md#purpose){:latex-href="#ref-SP800-63"} for details on how to choose the most appropriate FAL.
-->

Federation 実装時の選択肢は幅広いが, FAL はよりセキュアなデプロイメントに関する明示的なガイダンスを提供することを意図している.
最適な FAL の選択方法についての詳細は [[SP800-63]](../_sp800-63/sec1_purpose.ja.md#purpose){:latex-href="#ref-SP800-63"} を参照のこと.

<!--
Each FAL is characterized by a set of requirements that increase the security and complexity as the FAL increases. These requirements are listed here and expanded in other sections of this document:
-->

FAL は, レベルが上がるごとにセキュリティと複雑性が増すという特徴を持つ, 一連の要件の集合として表現される.
これらの要件については, 本セクションでリスト化したのち, 本ドキュメント各セクションで詳細化する.

<!--
Cryptographic Verifiability
: The assertion presented in the federation protocol is traceable back to a specific IdP that issued it, and that connection can be verified with a cryptographic mechanism such as a digital signature or MAC. This also allows the RP to verify that the assertion was not modified or forged. This is required at all FALs.
-->

Cryptographic Verifiability
: Federation Protocol において提示された Assertion が, それを発行した特定の IdP を追跡可能であり, その関係性を Digital Signature や MAC などの暗号論的メカニズムにより検証可能であること. また RP によって当該 Assertion が改変されたり偽造されていないことを検証できること. これは全ての FAL において求められる要件である.

<!--
Audience Restriction
: The assertion presented in the federation protocol is targeted to a specific RP and the RP can verify that it is the intended audience of the assertion. This is required at all FALs.
-->

Audience Restriction
: Federation Protocol において提示された Assertion が, 特定の RP に向けたものであり, 当該 RP が当該 Assertion の Audience を検証可能であること. これは全ての FAL において求められる要件である.

<!--
Injection Protection
: The RP is strongly protected from an attacker presenting an assertion in circumstances outside a current federation transaction request.
-->

Injection Protection
: Attacker が当該 Federation Transaction リクエスト外で得た Assertion を提示してくるような Attack に対して, RP が強固な保護策を持つこと.

<!--
Trust Agreement
: The IdP and RP have agreed to participate in a federation transaction with each other for the purposes of logging in the subscriber to the RP. This can be traced back to a static agreement between the parties or occur implicitly from the connection itself.
-->

Trust Agreement
: IdP と RP が, 双方ともに, 当該 Subscriber を当該 RP にログインさせるために当該 Federation Transaction に参加することに合意すること. これは両パーティー間の事前の静的な合意によることもあるし, 当該接続を持って暗黙的に合意したとみなされることもある.

<!--
Registration
: The IdP and RP have exchanged identifiers and key material to allow for the verification of assertions and other artifacts during future federation transactions.
-->

Registration
: IdP と RP が相互に自身の識別子とキーマテリアルを交換し, それ以降の Federation Transaction 内で Assertion や Artifact の Verification に用いることができるようにすること.

<!--
Presentation
: The assertion can be presented to the RP either on its own (as a bearer assertion) or in concert with a bound authenticator presented by the subscriber.
-->

Presentation
: Assertion がそれ単体で RP に (Bearer Assertion として) 提示されたり, Subscriber が提示する Authenticator と紐づけた形で提示されたりすること.

<!--
[Table 1](sec4_fal.md#table-1) provides a non-normative summary of aspects for each FAL. Each successive level subsumes and fulfills all requirements of lower levels (e.g., a federation process at FAL3 can be accepted at FAL2 or FAL1 since FAL3 satisfies all the requirements of these lower levels). Combinations not found in the [Table 1](sec4_fal.md#table-1) are possible but outside the scope of this volume.
-->

[Table 1](sec4_fal.ja.md#table-1) は各 FAL を要約したものである (non-normative).
各レベルは, それ以下のレベルの全要件を内包および満たす. (e.g., FAL3 は下位レベルの要件をすべて満たしているため, FAL3 を満たしていれば, FAL2 や FAL1 の全ての要件を満たしている.)
[Table 1](sec4_fal.ja.md#table-1) に存在しない組み合わせも可能であるが, そういった組み合わせに関しては本ドキュメントのスコープ外とする.

[Table 1 Federation Assertion Levels](sec4_fal.ja.md#table-1){:name="table-1"}
{:latex-ignore="true"}

|FAL|Injection Protection|Trust Agreement|Registration|Presentation|
|:--:|----|----|----|----|----|----|
|1|Recommended|Dynamic or Static|Dynamic or Static|Bearer Assertion|
|2|Required|Static|Dynamic or Static|Bearer Assertion|
|3|Required|Static|Static|Assertion and Bound Authenticator|
{:latex-table="1" latex-caption="Federation Assurance Levels" latex-columns="p@0.05\textwidth,p@0.16\textwidth,p@0.13\textwidth,p@0.15\textwidth,p@0.25\textwidth"}

<!--
At all FALs, all assertions **SHALL** be used with a federation protocol as described in [Sec. 5](sec5_federation.md#federation). All assertions **SHALL** comply with the detailed requirements in [Sec. 6](sec6_assertions.md#assertions). All assertions **SHALL** be presented using one of the methods described in [Sec. 7](sec7_presentation.md#presentation). Examples of assertions used in federated protocols include the ID Token in OpenID Connect [[OIDC]](references.md#ref-OIDC) and assertions written in the Security Assertion Markup Language [[SAML]](references.md#ref-SAML).
-->

いかなる FAL においても, 全ての Assertion は [Sec. 5](sec5_federation.ja.md#federation) にあるように Federation Protocol とともに利用せねばならない (**SHALL**).
全ての Assertion は [Sec. 6](sec6_assertions.ja.md#assertions) に述べる要件を満たさねばならない (**SHALL**).
全ての Assertion は [Sec. 7](sec7_presentation.ja.md#presentation) に述べるいずれかの方法で提示されなければならない (**SHALL**).
Federation Protocol で利用される Assertion の例としては, OpenID Connect [[OIDC]](references.ja.md#ref-OIDC) における ID Token や Security Assertion Markup Language [[SAML]](references.ja.md#ref-SAML) に従って記述された Assertion などが挙げられる.

<!--
At all FALs, the IdP **SHALL** employ appropriately tailored security controls (to include control enhancements) from the moderate or high baseline of security controls defined in [[SP800-53]](references.md#ref-SP800-53) or equivalent federal (e.g., [[FEDRAMP]](references.md#ref-FEDRAMP)) or industry standard.
-->

いかなる FAL においても, IdP は, [[SP800-53]](references.ja.md#ref-SP800-53) や同等の連邦標準 (e.g., [[FEDRAMP]](references.ja.md#ref-FEDRAMP)) および業界標準において定義された中程度ないしは高度なベースラインを構成するセキュリティコントロールの中から, 適切に調整されたセキュリティコントロールを採用しなければならない (**SHALL**).

## Federation Assurance Level 1 (FAL1) {#fal1}

<!--
At FAL1, the assertion being generated by the IdP **SHALL** meet a core set of requirements defined in [Sec. 6](sec6_assertions.md#assertions), including protection against modification or construction by an attacker by having the assertion contents signed by the IdP using approved cryptography. An RP **SHALL** verify the origin and integrity of the assertion upon receipt, as discussed in [Sec. 6](sec6_assertions.md#assertions), ensuring that the assertion has originated from the expected source.
-->

FAL1 では, IdP が生成する Assertion は [Sec. 6](sec6_assertions.ja.md#assertions) のコアとなる要件を満たさねばならない (**SHALL**).
これらの要件には, IdP が Approved Cryptography を用いて Assertion の内容に署名を施すことによる, Attacker からの Assertion 改変および偽造に対する保護策が含まれる.
RP は, [Sec. 6](sec6_assertions.ja.md#assertions) にあるように, Assertion を受け取った際はその起源や Integrity (完全性) を検証し, それが期待した出所を起源としたものであることを保証せねばならない (**SHALL**).

<!--
All assertions at FAL1 **SHALL** be audience-restricted to a specific RP or set of RPs, and the RP **SHALL** validate that it is one of the targeted RPs for the given assertion. The IdP **SHALL** ensure that any party holding the assertion, including the RP, is unable to impersonate the IdP at a non-targeted RP by protecting the assertion with a signature and key using approved cryptography. If the assertion is protected by a digital signature using an asymmetric key, the IdP **MAY** use the same public and private key pair to sign assertions to multiple RPs. The IdP **MAY** publish its public key in a verifiable fashion, such as at an HTTPS-protected URL at a well-known location. If the assertion is protected by a keyed message authentication code (MAC) using a shared key, the IdP **SHALL** use a different shared key for each RP.
-->

FAL1 における Assertion は全て, 特定の RP (群) に対する Audience Restriction が施されなければならず (**SHALL**), RP が当該 Assertion の Audience に自身が含まれていることを確認せねばならない (**SHALL**).
IdP は, Approved Cryptography による署名及び鍵を用いて当該 Assertion を保護し, 当該 RP を含む全ての Assertion 所有者が IdP になりすますことができないようにせねばならない (**SHALL**).
Assertion が Asymmetric Key を用いた Digital Signature により保護されている場合は, IdP は同じ Public & Private Key ペアを用いて複数の RP に向けて Assertion に署名を行っても良い (**MAY**).
IdP は, HTTPS で保護された well-known location を用いるなど, 検証可能な形で自身の Public Key を公開してもよい (**MAY**).
Assertion が Shared Secret を用いた鍵付き Message Authentication Code (MAC) により保護されている場合は, IdP は RP 毎に異なる Shared Secret を用いなければならない (**SHALL**).

<!--
At FAL1, the trust agreement between the IdP and RP **MAY** be established entirely dynamically. For instance, the subscriber can identify their chosen IdP to the RP at runtime, allowing the RP to discover the IdP's parameters and register itself for use by the subscriber. The subscriber is prompted by the IdP to determine which attributes are released to the RP, and for what purposes. In this example, the trust between the IdP and RP is driven entirely by the desires and actions of the subscriber. Note that at FAL1, it is still possible for the trust agreement and registration to happen statically.
-->

FAL1 では IdP-RP 間の Trust Agreement は完全に Dynamic に確立しうる (**MAY**).
例えば, Subscriber が RP に対して動的に IdP を選択・指定し, RP は IdP のパラメータを Discovery により取得し自身を IdP に登録することも可能である.
IdP は Subscriber に対してどの Attributre を何の目的で RP に提示するかを選択させる.
こういった例では, IdP-RP 間の信頼関係は完全に Subscriber の要求および行動により主導される.
なお FAL1 でも Static な Trust Agreement および Registration が可能であることは留意.

<!--
In existing federation protocols, FAL1 can be implemented with the OpenID Connect Implicit Client profile [[OIDC-Implicit]](references.md#ref-OIDC-implicit), the OpenID Connect Hybrid Client profile in [[OIDC]](references.md#ref-OIDC), or the SAML Web SSO [[SAML-WebSSO]](references.md#ref-SAML-websso) profile with no additional features. In each of these profiles, the assertion is signed by the IdP and the RP is identified in a portion of the assertion covered by the signature.
-->

既存の Federation Protocol では, FAL1 は OpenID Connect Implicit Client プロファイル [[OIDC-Implicit]](references.ja.md#ref-OIDC-implicit), OpenID Connect Hybrid Client プロファイル [[OIDC]](references.ja.md#ref-OIDC), 追加機能なしの SAML Web SSO プロファイル [[SAML-WebSSO]](references.ja.md#ref-SAML-websso) などにより実装可能である.
これらのプロファイルでは, Assertion は IdP により署名され, RP は署名された Assertion の内容により指定される.

## Federation Assurance Level 2 (FAL2) {#fal2}

<!--
All the requirements for FAL1 apply at FAL2 except where overridden by more specific or stringent requirements here.
-->

FAL1 に対する要件は, ここでより明確ないし厳密にオーバーライトされない限り全て FAL2 でも求められる.

<!--
At FAL2, the assertion **SHALL** also be strongly protected from being injected by an attacker. To accomplish this, the assertion **SHOULD** be presented using back channel presentation as discussed in [Sec. 7.1](sec7_presentation.md#back-channel), as in the OpenID Connect Basic Client profile [[OIDC-Basic]](references.md#ref-OIDC-basic). In this presentation method, the RP fetches the assertion directly from the IdP by using a single-use assertion reference, thereby preventing an attacker from injecting the assertions through an external access point. If front channel presentation is used as discussed in [Sec. 7.2](sec7_presentation.md#front-channel), additional injection protections **SHALL** be implemented by the RP.
-->

FAL2 では Assertion は Attacker による Injection Attack から強固に保護される必要がある (**SHALL**).
この要件を満たすためには, Assertion は [Sec. 7.1](sec7_presentation.ja.md#back-channel) にあるように, OpenID Connect Basic Client プロファイル [[OIDC-Basic]](references.ja.md#ref-OIDC-basic) などを用いて, Back-Channel で提示されるべきである (**SHOULD**).
この提示方法では, RP はワンタイムな Assertion Reference を用いて IdP から直接 Assertion を取得する.
従って Attacker は外部アクセスポイントを通じて Assertion を Inject することはできない.
[Sec. 7.2](sec7_presentation.ja.md#front-channel) のような Front-Channel による提示では, RP は追加の Injection Protection を実装しなければならない (**SHALL**).

<!--
Regardless of the presentation method used, injection attacks can be further mitigated by always requiring that the federation transaction start at the RP instead of being initiated by the IdP, thereby allowing the RP to associate an incoming assertion with a specific request that the subscriber initiated within a continuous session.
-->

Assertion の提示方法の如何を問わず, Injection Attack は Federation Transaction を常に IdP からではなく RP から開始することで防ぐこともできる.
これにより, RP は取得される Assertion をある Session 内において Subscriber が開始した特定のリクエストと紐づけることができる.

<!--
At FAL2, the trust agreement between the IdP and RP **SHALL** be established statically, including establishing limits of which attributes are made available to the RP and for what purpose. This trust agreement **MAY** be bilateral between the IdP and RP or **MAY** be managed through the use of a multilateral federation partnership. The registration **MAY** be dynamic, provided that the RP and IdP can prove their connection at runtime to the established trust agreement between them. Such methods for this proof vary by federation protocol, but can include presentation of software attestations and proof of control over URLs at trusted domains.
-->

FAL2 では, IdP-RP 間の Trust Agreement は Static に確立されなければならない (**SHALL**).
これには RP に提示可能な Attribute 及びその利用目的の制限の確立も含む.
Trust Agreement は IdP-RP の二者間 (Bilateral) で確立することもできるし (**MAY**), 多者間 (Multilateral) での Federation パートナーシップを介して確立することもできる (**MAY**).
RPと IdP が実行時に確立済の Trust Agreement を証明可能であれば, Registration は Dynamic でもよい (**MAY**).
そのような証明方法は Federation Protocol により多様であるが, Software Attestation の提示や Trusted Domain 上の URL の管理権限を証明することなどが例として挙げられる.

<!--
Government-operated IdPs asserting authentication at FAL2 **SHALL** protect keys used for signing or encrypting those assertions with mechanisms validated at [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher.
-->

政府が運営する IdP のうち FAL2 での Authentication を提供する IdP は, Assertion の署名及び暗号化に用いる鍵を [[FIPS140]](references.ja.md#ref-FIPS140) Level 1 およびそれ以上の手法により保護しなければならない (**SHALL**).

## Federation Assurance Level 3 (FAL3) {#fal3}

<!--
All the requirements at FAL1 and FAL2 apply at FAL3 except where overridden by more specific or stringent requirements here.
-->

FAL1 および FAL2 に対する要件は, ここでより明確ないし厳密にオーバーライトされない限り全て FAL3 でも求められる.

<!--
At FAL3, the subscriber **SHALL** authenticate to the RP by presenting an authenticator directly to the RP in addition to presenting an assertion. The authenticator presented is known as a _bound authenticator_, described in [Sec. 6.1.2](sec6_assertions.md#boundauth). For example, the subscriber goes through a federated login process at the IdP and RP, and the RP then prompts the subscriber for a bound authenticator that is associated with that RP subscriber account. The bound authenticator presented at FAL3 need not be the same authenticator used by the subscriber to authenticate to the IdP. The assertion is used to identify the subscriber to the RP while the bound authenticator gives very high assurance that the party attempting to log in is the subscriber identified in the assertion. FAL3 is not reached at the RP until the subscriber authenticates with the bound authenticator and the RP verifies that the authenticator presented is correctly bound to the RP subscriber account identified by the assertion.
-->

FAL3 では Subscriber は Assertion に加えて Authenticator を Direct に RP に提示することで Authenticate せねばならない (**SHALL**).
ここで用いられる Authenticator は _Bound Authenticator_ とも呼ばれ, [Sec. 6.1.2](sec6_assertions.ja.md#boundauth) に後述される.
例えば Subscriber が IdP と RP の間で Federation によるログインプロセスを実施する場合, RP は Subscriber に RP Subscriber Account に紐づく Bound Authenticator の提示を促す.
FAL3 で提示される Bound Authenticator は Subscriber が IdP に Authenticate する際に用いられる Authenticator と同一である必要はない.
Assertion は RP が Subscriber を識別する際に用いられるが, その際に Bound Authenticator はログインしようとしている当事者が Assertion により識別される Subscriber であるという高い確度を与える.
なお, Subscriber が Bound Authenticator を用いて Authenticate し, RP が当該 Authenticator が正しく当該 Assertion が示す RP Subscriber Account に紐づいていることを検証するまで, FAL3 が達成されることはない.

<!--
At FAL3, the trust agreement and registration between the IdP and RP **SHALL** be established statically. All identifying key material and federation parameters for all parties  (including the list of attributes sent to the RP) **SHALL** be fixed ahead of time, before the federated authentication process can take place. Runtime decisions **MAY** be used to further limit what is sent between parties in the federated authentication process (e.g., a runtime decision could opt to not disclose an email address even though this attribute was included in the parameters of the trust agreement).
-->

FAL3 では, IdP-RP 間の Trust Agreement および Registration は Static に確立されなければならない (**SHALL**).
全当事者にとって, 識別に用いられるキーマテリアルおよび Federation パラメータ (RP に送信される Attribute リストを含む) は, Federation による Authentication プロセス実施前に固定されていなければならない (**SHALL**).
Federation による Authentication プロセスの中で送信する項目をさらに制限する場合には, 動的に決定がなされてもよい (**MAY**).
(e.g., Trust Agreement で合意されたパラメータには含まれているものの Email Address を開示したくない場合など)

<!--
IdPs asserting authentication at FAL3 **SHALL** protect keys used for signing or encrypting those assertions with mechanisms validated at [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher.
-->

FAL3 での Authentication を提供する IdP は, Assertion の署名及び暗号化に用いる鍵を [[FIPS140]](references.ja.md#ref-FIPS140) Level 1 およびそれ以上の手法により保護しなければならない (**SHALL**).

## Requesting and Processing xALs {#request-xals}

<!--
Since an IdP is capable of asserting the identities of many different subscribers with a variety of authenticators using a variety of federation parameters, the IAL, AAL, and FAL could vary across different federated logins, even to the same RP.
-->

IdP は, 多様な Federation パラメータおよび Authenticator を用いて, 多数の Subscriber の Identity を主張することができる.
従って同一の RP に対しても異なる Federation ログイン毎に IAL, AAL および FAL は変わりうる.

<!--
The RP **SHALL** be informed of the following information for each federated transaction:
-->

RP は各 Federation Transaction 毎に以下の情報を知らされなければならない (**SHALL**).

<!--
- The IAL of the subscriber account being presented to the RP, or an indication that no IAL claim is being made
- The AAL of the currently active session of the subscriber at the IdP, or an indication that no AAL claim is being made
- The FAL of the federated transaction
-->

- RP に提示される Subscriber Account の IAL. これがない場合は IAL に関する主張がないことを示唆するものとする.
- IdP における当該 Subscriber の当該アクティブ Session の AAL. これがない場合は AAL に関する主張がないことを示唆するものとする.
- 当該 Federation Transaction の FAL.

<!--
The RP gets this xAL information from a combination of parameters in the trust agreement as described in [Sec. 5.1](sec5_federation.md#trust-agreement#trust-agreement) and information included in the assertion as described in [Sec. 6](sec6_assertions.md#assertions). If the xAL is unchanging for all messages between the IdP and RP, the xAL information **SHALL** be included in the parameters of the trust agreement between the IdP and RP. If the xAL varies, the information **SHALL** be included as part of the assertion as discussed in [Sec. 6](sec6_assertions.md#assertions).
-->

RP は上記 xAL 情報を [Sec. 5.1](sec5_federation.ja.md#trust-agreement#trust-agreement) に述べる Trust Agreement のパラメータおよび [Sec. 6](sec6_assertions.ja.md#assertions) に述べる Assertion に含まれる情報の組み合わせにより取得する.
IdP-RP 間の全メッセージで xAL が不変な場合は, xAL 情報は IdP-RP 間の Trust Agreement のパラメータに含まれることとする (**SHALL**).
xAL が可変の場合は, [Sec. 6](sec6_assertions.ja.md#assertions) に述べる Assertion の一部として xAL 情報を含むものとする (**SHALL**).

<!--
The IdP **MAY** indicate that no claim is made to the IAL or AAL for a given federation transaction. In such cases, no default value is assigned to the resulting xAL. That is to say, a federation transaction without an IAL declaration in either the trust agreement or the assertion is functionally considered to have "no IAL" and the RP cannot assume the account meets "IAL1", the lowest numbered IAL described in this suite.
-->

IdP は所与の Federation Transaction に対していかなる IAL ないし AAL に関する主張もないことを示唆しても良い (**MAY**).
この場合, 当該 Transaction の結果としての xAL には何のデフォルト値も割り当てられることはない.
つまり, Trust Agreement にも Assertion にも IAL に関する宣言のない Federation Transaction は "IAL を持たない" ものとし, RP は当該アカウントが本ガイドライン群に規定する最低の IAL である "IAL1" を満たすものと仮定してはならない.

<!--
The RP **SHALL** determine the minimum IAL, AAL, and FAL it is willing to accept for access to any offered functionality. An RP **MAY** vary its functionality based on the IAL, AAL, and FAL of a specific federated authentication. For example, an RP can allow login at AAL2 for common functionality (e.g., viewing the status of a dam system) but require AAL3 be used for higher risk functionality (e.g., changing the flow rates of a dam system). Similarly, an RP could restrict management functionality to only certain subscriber accounts which have been identity proofed at IAL2, while allowing logins from all subscriber accounts regardless of IAL.
-->

RP は, 提供する機能に対する Access を受け入れるための最低限の IAL, AAL および FAL を規定しなければならない (**SHALL**).
RP は, 特定の Federated Authentication における IAL, AAL および FAL に基づいて, 提供する機能を変更しても良い (**MAY**).
例えば, AAL2 でのログインでは共通機能 (e.g., ダムシステムのステータス閲覧) へのアクセスのみとし, AAL3 ではよりハイリスクな機能 (e.g., ダムシステムの流量変更) へのアクセスを許可するなどが考えられる.
同様に, RP は, IAL の如何を問わず全 Subscriber Account によるログインを許可しつつも, 管理機能を IAL2 による Identity Proofing を経た特定の Subscriber Account のみに制限する, といったことも可能である.

<!--
In a federation process, only the IdP has direct access to the details of the subscriber account, which determines the applicable IAL, and the authentication event at the IdP, which determines the applicable AAL. Consequently, the RP **SHALL** consider the IdP's declaration of the IAL and AAL as the sole source of these levels for a given federated transaction.
-->

Federation プロセスにおいては, IdP のみが Subscriber Account に対して適切な IAL を決定するための詳細情報への直接の Access を持つ. また適切な AAL を決定するための IdP における Authentication イベントに関しても同様である.
従って, RP は所与の Federation Transaction における IdP による IAL および AAL の宣言を, それらのレベルの単一の情報源としなければならない (**SHALL**).

<!--
The RP **SHALL** ensure that the federation transaction meets the requirements of the FAL declared in the assertion. For example, the RP needs to ensure the presentation method meets the injection protection requirements at FAL2 and above, and that the appropriate bound authenticator is presented at FAL3.
-->

RP は Federation Transaction が Assertion に示される FAL 要件を満たすことを保証しなければならない (**SHALL**).
例えば, RP は Presentation 方法が FAL2 以上で求められる Injection Protection を満たし, FAL3 を満たす適切な Bound Authenticator が提示されたことを保証する必要がある, といったことが考えられる.

<!--
IdPs **SHALL** support a mechanism for RPs to specify a set of minimum acceptable xALs as part of the trust agreement and **SHOULD** support the RP specifying a more strict minimum set at a as part of the federation transaction. When an RP requests a particular xAL, the IdP **SHOULD** fulfill that request, if possible, and **SHALL** indicate the resulting xAL in the assertion. For example, if the subscriber has an active session that was authenticated at AAL1, but the RP has requested AAL2, the IdP needs to prompt the subscriber for AAL2 authentication to step up the security of the session at the IdP during the subscriber's interaction at the IdP, if possible. The IdP sends the resulting AAL as part of the returned assertion, whether it is AAL1 (the original session) or AAL2 (a stepped-up authentication).
-->

IdP は RP が Trust Agreement において許容可能な最低限の xAL を指定する仕組みをサポートせねばならず (**SHALL**), Federation Transaction においてより厳格な最低限の xAL を指定する仕組みもサポートすべきである (**SHOULD**).
RP が特定の xAL をリクエストした場合, IdP はそのリクエストを満たすべきであり (**SHOULD**), 可能であれば Assertion においてその結果の xAL を示すものとする (**SHALL**).
例えば, Subscriber が AAL1 で Authenticate されたアクティブな Session を持つ一方で RP が AAL2 を要求している場合, IdP は可能であれば Subscriber に AAL2 での Authentication を促し, IdP とのインタラクションを通じて当該 Session のセキュリティを高める必要がある.
IdP は, 結果として得られた AAL を, 返却する Assertion に含める. これは AAL1 (元の Session の AAL) ないし AAL2 (より強固な Authentication で得られた AAL) となるであろう.