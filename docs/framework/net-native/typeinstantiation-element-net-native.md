---
title: "&lt;TypeInstantiation&gt; Element (.NET Native) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5eada64-075b-4162-9655-ded84e4681f2
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# &lt;TypeInstantiation&gt; Element (.NET Native)
Wendet eine Laufzeitreflektionsrichtlinie auf einen konstruierten generischen Typ an.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<TypeInstantiation Name="type_name"  
                   Arguments="type_arguments"  
                   Activate="policy_type"  
                   Browse="policy_type"  
                   Dynamic="policy_type"  
                   Serialize="policy_type"  
                   DataContractSerializer="policy_setting"  
                   DataContractJsonSerializer="policy_setting"  
                   XmlSerializer="policy_setting"  
                   MarshalObject="policy_setting"  
                   MarshalDelegate="policy_setting"  
                   MarshalStructure="policy_setting" />  
  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Attributtyp|Beschreibung|  
|---------------|--------------------|-----------------|  
|`Name`|Allgemein|Erforderliches Attribut. Gibt den Typnamen an.|  
|`Arguments`|Allgemein|Erforderliches Attribut. Gibt die generischen Typargumente an. Wenn mehrere Argumente vorhanden sind, werden sie durch Kommas getrennt.|  
|`Activate`|Spiegelung|Optionales Attribut. Steuert den Laufzeitzugriff auf Konstruktoren, um die Aktivierung von Instanzen zu ermöglichen.|  
|`Browse`|Spiegelung|Optionales Attribut. Steuert das Abfragen von Informationen über Programmelemente, ermöglicht jedoch keinen Laufzeitzugriff.|  
|`Dynamic`|Spiegelung|Optionales Attribut. Steuert den Laufzeitzugriff auf alle Typmember, einschließlich Konstruktoren, Methoden, Felder, Eigenschaften und Ereignisse, um die dynamische Programmierung zu ermöglichen.|  
|`Serialize`|Serialisierung|Optionales Attribut. Steuert den Laufzeitzugriff auf Konstruktoren, Felder und Eigenschaften, um Serialisierung und Deserialisierung von Typinstanzen durch Bibliotheken wie das Newtonsoft JSON-Serialisierungsprogramm zu ermöglichen.|  
|`DataContractSerializer`|Serialisierung|Optionales Attribut. Steuert die Richtlinie für die Serialisierung, die mithilfe der <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> Klasse.|  
|`DataContractJsonSerializer`|Serialisierung|Optionales Attribut. Steuert die Richtlinie für die JSON-Serialisierung verwendet die <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> Klasse.|  
|`XmlSerializer`|Serialisierung|Optionales Attribut. Steuert die Richtlinie für die XML-Serialisierung, die verwendet die <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> Klasse.|  
|`MarshalObject`|Interop|Optionales Attribut. Steuert die Richtlinie für das Marshalling von Verweistypen zu Windows-Runtime und COM.|  
|`MarshalDelegate`|Interop|Optionales Attribut. Steuert die Richtlinie für das Marshalling von Delegattypen als Funktionszeiger zu systemeigenem Code.|  
|`MarshalStructure`|Interop|Optionales Attribut. Steuert die Richtlinie für das Marshalling von Strukturen zu systemeigenem Code.|  
  
## <a name="name-attribute"></a>Namensattribut  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|*TYPE_NAME*|Der Typname. Wenn diese `<TypeInstantiation>` Element untergeordnet ist ein [ <> \> ](../../../docs/framework/net-native/namespace-element-net-native.md) -Element, ein [ <> \> ](../../../docs/framework/net-native/type-element-net-native.md) Elements oder eines anderen `<TypeInstantiation>` Element, *Type_name* können den Namen des Typs ohne den Namespace angeben. Andernfalls *Type_name* muss den vollqualifizierten Typnamen enthalten. Der Typname wird nicht ergänzt. Z. B. für eine <xref:System.Collections.Generic.List%601?displayProperty=fullName> -Objekt, das `<TypeInstantiation>` Element könnte wie folgt aussehen:<br /><br /> `\<TypeInstantiation Name=System.Collections.Generic.List Dynamic="Required Public" />`|  
  
## <a name="arguments-attribute"></a>Arguments-Attribut  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|*type_argument*|Gibt die generischen Typargumente an. Wenn mehrere Argumente vorhanden sind, werden sie durch Kommas getrennt. Jedes Argument muss aus dem vollqualifizierten Typnamen bestehen.|  
  
## <a name="all-other-attributes"></a>Alle anderen Attribute  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|*policy_setting*|Die Einstellung, die auf diesen Richtlinientyp für den konstruierten generischen Typ anzuwenden ist. Mögliche Werte sind `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` und `Required All`. Weitere Informationen finden Sie unter [Laufzeitrichtlinieneinstellungen der Richtlinie](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/event-element-net-native.md)|Wendet die Reflektionsrichtlinie auf ein Ereignis dieses Typs an.|  
|[<>\>](../../../docs/framework/net-native/field-element-net-native.md)|Wendet die Reflektionsrichtlinie auf ein Feld dieses Typs an.|  
|[<>\>](../../../docs/framework/net-native/impliestype-element-net-native.md)|Wendet eine Richtlinie auf einen Typ an, wenn diese Richtlinie an den Typ angewendet wurde, der vom enthaltenden `<TypeInstantiation>`-Element dargestellt wird.|  
|[<>\>](../../../docs/framework/net-native/method-element-net-native.md)|Wendet die Reflektionsrichtlinie auf eine Methode dieses Typs an.|  
|[<>\>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)|Wendet die Reflektionsrichtlinie auf eine konstruierte generische Methode dieses Typs an.|  
|[<>\>](../../../docs/framework/net-native/property-element-net-native.md)|Wendet die Reflektionsrichtlinie auf eine Eigenschaft dieses Typs an.|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Wendet die Reflektionsrichtlinie auf einen geschachtelten Typ an.|  
|`<TypeInstantiation>`|Wendet die Reflektionsrichtlinie auf einen geschachtelten konstruierten generischen Typ an.|  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[<>\>](../../../docs/framework/net-native/application-element-net-native.md)|Dient als Container für anwendungsweite Typen und Typmember, deren Metadaten zur Laufzeit für die Reflektion verfügbar sind.|  
|[<>\>](../../../docs/framework/net-native/assembly-element-net-native.md)|Wendet die Reflektionsrichtlinie auf alle Typen in einer angegebenen Assembly an.|  
|[<>\>](../../../docs/framework/net-native/library-element-net-native.md)|Definiert die Assembly, die Typen und Typmember enthält, deren Metadaten zur Laufzeit für die Reflektion verfügbar sind.|  
|[<>\>](../../../docs/framework/net-native/namespace-element-net-native.md)|Wendet die Reflektionsrichtlinie auf alle Typen in einem Namespace an.|  
|[<>\>](../../../docs/framework/net-native/type-element-net-native.md)|Wendet die Reflektionsrichtlinie auf einen Typ und alle seine Member an.|  
|`<TypeInstantiation>`|Wendet die Reflektionsrichtlinie auf einen konstruierten generischen Typ und alle seine Member an.|  
  
## <a name="remarks"></a>Hinweise  
 Die Reflektions-, Serialisierungs- und Interop-Attribute sind optional. Allerdings muss mindestens eines vorhanden sein.  
  
 Wenn ein `<TypeInstantiation>` Element ist das untergeordnete Element ein [ <> \</> \> ](../../../docs/framework/net-native/assembly-element-net-native.md), [ <> \</> \> ](../../../docs/framework/net-native/namespace-element-net-native.md), oder [ <> \</> \> ](../../../docs/framework/net-native/type-element-net-native.md), Elements ist, überschreibt es die vom übergeordneten Element definierten Richtlinieneinstellungen. Wenn ein [ <> \> ](../../../docs/framework/net-native/type-element-net-native.md) Element definiert eine entsprechende generische Typdefinition der `<TypeInstantiation>` -Element überschreibt die laufzeitreflektionsrichtlinie nur für Instanziierungen des angegebenen konstruierten generischen Typs.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird Reflektion zum Abrufen der generischen Typdefinition von einem konstruierten <xref:System.Collections.Generic.Dictionary%602> Objekt.</TKey, TValue> Darüber hinaus verwendet Reflektion zum Anzeigen von Informationen über <xref:System.Type> Objekte, die konstruierte generische Typen und generische Typdefinitionen darstellen. Die Variable `b` in diesem Beispiel ist ein [TextBlock](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) Steuerelement.  
  
 [!code-csharp[ProjectN_Reflection#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/makegenerictype1.cs#2)]  
  
 Nach der Kompilierung mit der [!INCLUDE[net_native](../../../includes/net-native-md.md)] -toolkette löst das Beispiel eine [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) Ausnahme in der Zeile, die Aufrufe der <xref:System.Type.GetGenericTypeDefinition%2A?displayProperty=fullName> Methode. Sie können die Ausnahme eliminieren und die erforderlichen Metadaten bereitstellen, indem Sie folgendes `<TypeInstantiation>`-Element in der Laufzeitdirektivendatei hinzufügen:  
  
```xml  
  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
    <Assembly Name="*Application*" Dynamic="Required All" />  
     <TypeInstantiation Name="System.Collections.Generic.Dictionary"  
                        Arguments="System.String,GenericType.Example"  
                        Dynamic="Required Public" />  
  </Application>  
</Directives>  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Laufzeit-Konfigurationsdatei Laufzeitdirektiven (rd.xml) Referenz](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Elemente der Laufzeitrichtlinie](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [Richtlinie für die Laufzeitrichtlinie](../../../docs/framework/net-native/runtime-directive-policy-settings.md)