# Filters
フィルタは、データオブジェクトに対し、ある基準を満たしているかどうかのテストを行います。例えば、フィルタを含むコンポーネントは、フィルタの条件が満たされる時のみに実行されます。

## 典型
典型的なフィルタは4つのパラメータで構成されています。  

name : 条件名(テスト名)  
domain : テストが実行される領域(例えば、防具スロットなど)  
operator : 値を比較する演算子  
value : テストで比較する値  

一般的なフィルタは、次のように記述します。  

```json
{ "test" : "moon_intensity", "subject" : "self", "operator" : "greater", "value" : "0.5" }
```

このフィルタは、このフィルタを呼び出したエンティティ(self)が、その場所でmoon_intensityをテストし、結果が0.5より大きい場合は true (結果を満たしている)を返します。

## グループ
テストは、「all_of」, 「any_of」 という2つの識別子でグループにまとめることができます。  
「all_of」の場合、最終的にグループ内の全てのテストがtrueを返したときに、グループもtrueを返します。  
「any_of」の場合、グループ内のテストいずれかがtrueを返したときに、グループもtrueを返します。

[翻訳元](https://minecraft.gamepedia.com/Bedrock_Edition_entity_components_documentation#Filters)