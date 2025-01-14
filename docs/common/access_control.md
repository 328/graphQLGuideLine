# 不適切なアクセス制御

## 概要

GraphQL APIにおいても、ほかのシステムと同様に、アクセス制御を適切に実施する必要があります。

## 影響

GraphQL APIのアクセス制御が適切に実施されていない場合、APIで操作できるさまざまなリソース(例：ユーザー情報やライセンスキーなど)が、不まさに作成、取得、更新、削除される可能性があります。

昨今では、国内のサービスでも、GraphQL APIにおけるアクセス制御の不備が発見され、報告されています。詳しくは、下記のページをご覧ください。

- [GraphQL採用サービスで任意カラムを取得できる脆弱性を見つけた話](https://zenn.dev/mipsparc/articles/a818970a19ade6)
- [GraphQL採用サービスに追加で脆弱性を報告した話](https://gist.github.com/mala/8f264786026d105c7144dcbed8240bc9)

## 検証方法

対象のリソースに対するアクセス権を持たない認証状態で、クエリやミューテーションを通じて、リソースのCRUD操作を試みてください。たとえば、ユーザーIDやライセンスキーのようなアクセス識別子を送っている場合は、値の追加や変更などの検証する方法があります。操作が成功した場合、適切なアクセス制御が実施されていない事がわかります。

## 対策

RBAC(**R**ole **B**ased **A**ccess **C**ontrol)やほかのアクセス制御のしくみを用いて、リソースにCRUDを実行しようとしているユーザーが、適切な権限を有しているかを必ず検証してください。もし、その操作が正規のユーザーによるものであることを確認できない場合、そのリクエストを拒否するようにしてください。
