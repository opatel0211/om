from odoo import models, fields, api
import pymongo

class MyModel(models.Model):
    _name = 'my.model'
    _description = 'My Model'

    name = fields.Char(string='Name')

    @api.model
    def create(self, values):
        # Connect to MongoDB
        client = pymongo.MongoClient('mongodb://localhost:27017/')
        db = client['your_mongodb_database_name']

        # Insert data into MongoDB
        collection = db['my_collection']
        collection.insert_one({'name': values.get('name')})

        # Continue with Odoo record creation
        return super(MyModel, self).create(values)
