```startuml
@startuml

/'
  図の中で目立たせたいエンティティに着色するための
  色の名前（定数）を定義できます。
  ↓色のサンプル↓
  https://github.com/shibakay/2021sys-design/blob/main/color.md
'/

!define MASTER_MARK_COLOR Orange 
!define TRANSACTION_MARK_COLOR DeepSkyBlue

'グラデーションさせる場合 #xx-xx
!define MAIN_ENTITY #MintCream-MistyRose

/'
  デフォルト色を"skinparam class"で設定します。
'/
skinparam class {
    '図の背景
    BackgroundColor Snow
    '図の枠
    BorderColor Black
    'リレーションの色
    ArrowColor Black
}

package "ECサイト" as target_system {
    /'
      マスターテーブルを M、トランザクションを T などで表記
      １文字なら "主" とか "従" まど日本語でも記載可能
     '/

    entity "会員" as customer <customers> <<M,MASTER_MARK_COLOR>> {
        +  c_id[PK]
        --
        c_name
        c_namek
        postcode
        c_address
        email
        c_birthday
        c_regdate
    }
    
 entity "商品" as prodact <prodact> <<T,TRANSACTION_MARK_COLOR>> MAIN_ENTITY{
    +p_id[PK]
    --
     p_name
     p_model
     gb_id[FK]
     gc_name
     gs_id
     m_id[FK]
     p_saledate
     p_price
    }
entity "販売メーカー" as maker <maker> <<T,TRANSACTION_MARK_COLOR>> MAIN_ENTITY{
    +m_id[PK]
    --
   m_name
   m_postcode
   m_address
   m_tel
   m_faxtel
   }
    entity "ジャンル" as genre <genre> <<M,MASTER_MARK_COLOR>> {
        +gb_id [PK]
        --
        gb_name
        gc_id
        gc_name
        gs_id
        gs_name
    }
 entity "パスワード" as category <m_category> <<M,MASTER_MARK_COLOR>> {
        + category_id [PK]
        --
        name
        reg_date
    }   
  }
 customer       |o-ri-o{     order
order          ||-ri-|{     order_detail
order_detail    }-do-||     items
items          }o-le-||     category 
@enduml
```
