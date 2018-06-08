# ios-review-ask-sample
アプリ利用率が高いユーザーに対してレビュー促進アラートを表示する。

## 概要

アプリ利用率が高いユーザーに対して、ボタン押下時にレビュー促進アラートを表示する。
ただし、一度レビュー促進アラートが表示されたユーザーには30日間表示させない。

## 実装方針

### アプリ利用率が高い」の表現

#### 対象ユーザー

10回以上アプリを開いたユーザーを対象とする。

#### レビュー促進アラート表示契機

- a: トップ画面の表示が10回目のとき
- b: 前回のレビュー促進アラート表示から30日後

## 詳細設計
### ReviewRequestController
レビュー依頼イベントの管理を行う。

#### プロパティ

##### アプリを開いた回数 

var launchedTimes: Int = 0

10になったらlaunchedApp10Timesを呼ぶ。

##### 最後にレビュー促進アラートを表示した日時
var dateShowReviewRequest: Date?
~~セットされたら、30日後にself.showReviewRequestを呼ぶ。~~
セットされたら、

##### 
##### アラート表示デリゲート
weak var reviewRequestDelegate: ReviewRequestDelegate

#### メソッド
- launchedApp10Times
10回アプリが開かれたときに呼ばれるメソッド
showReviewRequestを呼ぶ。

- showReviewRequest
delegate.showReviewRequestView
dateShowReviewRequest = Date()


### ReviewRequestDelegate

ReviewRequestControllerから依頼を受けてレビュー促進アラートを表示する。

- showReviewRequestView

### TopViewController: ReviewRequestDelegate
- ReviewRequestControllerを保持する。
-　アプリが開かれるたびにReviewRequestController.launchedTimesを１増やす
- ReviewRequestDelegateに準拠する
 
## 参考

- [SKStoreReviewController - StoreKit | Apple Developer Documentation](https://developer.apple.com/documentation/storekit/skstorereviewcontroller/)
- [sahara-ooga/ios-SKStoreReviewController-sample: review request dialog sample](https://github.com/sahara-ooga/ios-SKStoreReviewController-sample/tree/master)
