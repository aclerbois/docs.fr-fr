### <a name="xmlserializer-serializes-fields-differently-in-net-framework-45"></a>XmlSerializer sérialise les champs différemment dans .NET Framework 4.5

|   |   |
|---|---|
|Détails|Les changements au sein de <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> dans .NET Framework 4.5 ont entraîné une autre mise en forme des champs dans le code XML sérialisé.|
|Suggestion|Ce comportement a été corrigé dans une mise à jour de maintenance de .NET Framework 4.5. Pour résoudre ce problème, mettez à jour .NET Framework 4.5 ou mettez-le à niveau vers .NET Framework 4.5.1 ou version ultérieure. Sinon, le paramètre de configuration suivant sera restauré au comportement <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> 4.0 :<pre><code>&lt;system.xml.serialization&gt;&#13;&#10;&lt;xmlSerializer useLegacySerializerGeneration=&quot;true&quot; /&gt;&#13;&#10;&lt;/system.xml.serialization&gt;&#13;&#10;</code></pre>|
|Portée|Majeur|
|Version|4.5|
|Type|Runtime|
|API affectées|<ul><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.Stream%2CSystem.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.TextWriter%2CSystem.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Object%2CSystem.Xml.Serialization.XmlSerializationWriter)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.Stream%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.TextWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces%2CSystem.String)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter%2CSystem.Object%2CSystem.Xml.Serialization.XmlSerializerNamespaces%2CSystem.String%2CSystem.String)?displayProperty=nameWithType></li></ul>|
